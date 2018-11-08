# kubernetes
[Draft]

1) Start up machines using Vagrantfile
2) Add hostnames in /etc/hosts
3) Configure Certificates that will be used by cluster 
4) Install controller Binaries
5) Generate kube configs : kubeconfig files are used by a service or a user to authenticate oneself. 
   (service account kubeconfig / kube scheduler kubeconfig / admin kubeconfig)
6) Deploy etcd 
7) control plane deployment 
   Kubernetes control plane consist of: kube-apiserver , kube-controller-manager , kube-scheduler
   to verify  
       kubectl get componentstatuses --kubeconfig /etc/kubernetes/admin.kubeconfig

8) 
 



