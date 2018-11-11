# kubernetes
## Starting up machines
using 2 Vms with ubuntu bionic 

1 controller

1 worker

Start machines using Vagrantfile 

Edit /etc/hosts and make sure that both machines can ping each other

## Generate x509 certs 
https://github.com/mennahany93/kubernetes/tree/master/Certs

## Install controller Binaries  
 tag=v1.8.7
kube-apiserver , kube-controller-manager , kube-scheduler , kube-proxy , kubelet , kubectl 

5) Generate kube configs : kubeconfig files are used by a service or a user to authenticate oneself. 
   (service account kubeconfig / kube scheduler kubeconfig / admin kubeconfig)
6) Deploy etcd 
7) control plane deployment 
   Kubernetes control plane consist of: kube-apiserver , kube-controller-manager , kube-scheduler
   to verify  
       kubectl get componentstatuses --kubeconfig /etc/kubernetes/admin.kubeconfig

8) Prepare boostrapping part: Create the bootstrap token and kubeconfig which will be used by kubelets to
join the Kubernetes cluster
        Bootstrap token : 0b1f44.55917e1d261c6c2f

9)Expose CA and bootstrap kubeconfig via configmap 

10) Install Docker version used : 1.12
11) Install binaries on worker node v1.8.7


 



