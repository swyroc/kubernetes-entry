# Overview of minikube
* A all-in-one install of Kubernetes
* Takes all the distributed components of Kubernetes and packages them into a single virtual machine to run locally
* A few (important) caveats
* Minikube will be a Kubernetes cluster running on your machine
* You will use kubectl to connect to minikube as connect to Kubernetes clusters

# Installation of kubectl, kubelet, kubeadm, kubernetes-cni in China
Please refer to [Here](https://github.com/HuangMarco/knowledge-hub/blob/dev/linux-operation/linux_installation_softwares_components.md#kubernates).

# Installation of kubectl - Official

## Download the latest package for OS
Here I used CentOS.

```sh
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

# change modification
chmod +x kubectl

# copy to the path
mv kubectl /usr/local/bin/kubectl

# print the kubectl version
kubectl version

```

For more detail of the kubectl installation, please refer to [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/).


# Installation of minikube - Official
## Download the latest package for your OS
Here I used CentOS.

```sh
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube

# move minikube to the path
mv minikube /usr/local/bin/minikube
# check the version
minikube version
```

For more detail of the minikube installation, please refer to [here](https://kubernetes.io/docs/tasks/tools/install-minikube/).


# Installation of minikube - China
Because the outside network is slow and some websites are forbbiden, so we need to use the _minikube_ released by Aliyun.
<br>
For minikube in Aliyun, please refer to [Here](https://github.com/AliyunContainerService/minikube) and [Here](https://blog.csdn.net/CSDN_duomaomao/article/details/78568551).
You need to choose which version you need for minikube.

```sh
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v1.0.0/minikube-linux-amd64 \
  && chmod +x minikube

# move minikube to the path
mv minikube /usr/local/bin/minikube
# check the version
minikube version
```

# Resources

## Aliyun minikube

https://github.com/AliyunContainerService/minikube

## USTC Mirrors
https://mirrors.ustc.edu.cn/
<br>
https://mirrors.ustc.edu.cn/kubernetes/apt/pool/



