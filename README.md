# kubernetes
### Starting up machines
1. two controller machines
2. two worker machines
3. loadbalancer 

Manage all the work on kubernetes machine from local (client) machine 
### Install client tools 
1. cfssl 
2. kubectl 

### Generate certificates and distribute them 
Generate all certs needed locally using cfssl and then copy them to k8s servers 
https://github.com/mennahany93/kubernetes/tree/master/Certs
 
### Generate kubeconfigs 
kubeconfig files are used by a service or a user to authenticate oneself. enable k8 client to locate and authenticate with api-server
https://github.com/mennahany93/kubernetes/tree/master/kubeconfigs

### Generate Encryption key 
Kubernetes offers the ability to encrypt sensitive data when it is stored. However, in order to use this feature it is necessary to provide Kubernetes with a data encrpytion config containing an encryption key 

create this key , put it into config file then copy it to k8 controller servers 

Generate the Kubernetes Data encrpytion config file containing the encrpytion key:
```
ENCRYPTION_KEY=$(head -c 32 /dev/urandom | base64)

cat > encryption-config.yaml << EOF
kind: EncryptionConfig
apiVersion: v1
resources:
  - resources:
      - secrets
    providers:
      - aescbc:
          keys:
            - name: key1
              secret: ${ENCRYPTION_KEY}
      - identity: {}
EOF
```
Copy the file to both controller servers:
```
scp encryption-config.yaml user@<controller 1 public ip>:~/
scp encryption-config.yaml user@<controller 2 public ip>:~/
```

### Setting up etcd 
It is a distributed key value store that provides a way to store data across cluster of machines
https://github.com/mennahany93/kubernetes/tree/master/etcd



 



