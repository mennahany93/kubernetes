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


### Setting up control plane components
1. kube apiserver
2. controller manager
3. kube scheduler

### Installing control plane binaries
```
sudo mkdir -p /etc/kubernetes/config

wget -q --show-progress --https-only --timestamping \
  "https://storage.googleapis.com/kubernetes-release/release/v1.10.2/bin/linux/amd64/kube-apiserver" \
  "https://storage.googleapis.com/kubernetes-release/release/v1.10.2/bin/linux/amd64/kube-controller-manager" \
  "https://storage.googleapis.com/kubernetes-release/release/v1.10.2/bin/linux/amd64/kube-scheduler" \
  "https://storage.googleapis.com/kubernetes-release/release/v1.10.2/bin/linux/amd64/kubectl"

chmod +x kube-apiserver kube-controller-manager kube-scheduler kubectl

sudo mv kube-apiserver kube-controller-manager kube-scheduler kubectl /usr/local/bin/
```

### setting up kube-apiserver
https://github.com/mennahany93/kubernetes/tree/master/kube-apiserver

### setting up controller manager
https://github.com/mennahany93/kubernetes/tree/master/controller_manager

### setting up kube-scheduler

### Enable http health checks
Part of Kelsey Hightower's original Kubernetes the Hard Way guide involves setting up an nginx proxy on each controller to provide access to the Kubernetes API /healthz endpoint over http. This lesson explains the reasoning behind the inclusion of that step and guides you through the process of implementing the http /healthz proxy.
```
sudo apt-get install -y nginx
```
Create an nginx configuration for the health check proxy:
```
cat > kubernetes.default.svc.cluster.local << EOF
server {
  listen      80;
  server_name kubernetes.default.svc.cluster.local;

  location /healthz {
     proxy_pass                    https://127.0.0.1:6443/healthz;
     proxy_ssl_trusted_certificate /var/lib/kubernetes/ca.pem;
  }
}
EOF
```
Set up the proxy configuration so that it is loaded by nginx:
```
sudo mv kubernetes.default.svc.cluster.local /etc/nginx/sites-available/kubernetes.default.svc.cluster.local
sudo ln -s /etc/nginx/sites-available/kubernetes.default.svc.cluster.local /etc/nginx/sites-enabled/
sudo systemctl restart nginx
sudo systemctl enable nginx
```
You can verify that everything is working like so:
```
curl -H "Host: kubernetes.default.svc.cluster.local" -i http://127.0.0.1/healthz
```
