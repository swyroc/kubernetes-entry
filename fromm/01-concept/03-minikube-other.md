# Minikube
在单机上模拟一个K8S环境，使用Minikube可以在本地帮助搭建一个K8S环境，一般用于本地K8S开发学习用途等。对于维护真正完整意义的K8S来说,minikube是不够用的。

# Kubeadm
通过使用kubeadm来部署整个K8S环境，而如果要使用kubeadm，那么必须要准备2个程序包：kubeadm, kubelet，因为要在每个节点上运行pod，所以我们依然需要docker。




