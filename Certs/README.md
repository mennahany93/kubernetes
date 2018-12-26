# Locally generate CA cert 

1) **Create openssl configuration file** in /etc/kubernetes/pki directory 
2) **Kubernetes CA cert** used to sign the rest of k8 certs
3) **kube apiserver cert** gives 2 files kube-apiserver.crt and kube-apiserver.key
4) **apiserver kubelet client cert** used for x509 client authentication to the kubelet's HTTPS endpoint.
5) **admin client cert** used by a human to administrate the cluster.
6) **Service Account key**
7) **kube-scheduler cert**used to allow access to the resources required by the kube-scheduler component.
8) **front proxy CA cert** used to sign front proxy client cert.
9) **front proxy client cert** 
10) **kube-proxy cert**
11) **etcd CA cert**
12) **etcd cert**
13) **etcd peer cert**

Commands to Generate all certs 
https://nixaid.com/deploying-kubernetes-cluster-from-scratch/ 

