# kubernetes
## Starting up machines
1. two controller machines
2. two worker machines
3. loadbalancer 

Manage all the work on kubernetes machine from local (client) machine 
### Install client tools 
1. cfssl 
2. kubectl 

### Generate certificates and distribute them 
https://github.com/mennahany93/kubernetes/tree/master/Certs
 

Edit /etc/hosts and make sure that both machines can ping each other

## Generate x509 certs 
https://github.com/mennahany93/kubernetes/tree/master/Certs

## Install controller Binaries  
 tag=v1.8.7
 
kube-apiserver , kube-controller-manager , kube-scheduler , kube-proxy , kubelet , kubectl 

## Generate kube configs 
kubeconfig files are used by a service or a user to authenticate oneself. enable k8 client to locate and authenticate with api-server 

Generated on **Controller node**
https://github.com/mennahany93/kubernetes/tree/master/kubeconfigs

## Deploy etcd 

## control plane deployment 
   Kubernetes control plane consist of: kube-apiserver , kube-controller-manager , kube-scheduler
   to verify  
       
       * export KUBECONFIG=/etc/kubernetes/admin.kubeconfig*
       *kubectl get componentstatuses --kubeconfig /etc/kubernetes/admin.kubeconfig*

8) Prepare boostrapping part: Create the bootstrap token and kubeconfig which will be used by kubelets to
join the Kubernetes cluster
        Bootstrap token : 0b1f44.55917e1d261c6c2f

9)Expose CA and bootstrap kubeconfig via configmap 

10) Install Docker version used : 1.12
11) Install binaries on worker node v1.8.7


 



