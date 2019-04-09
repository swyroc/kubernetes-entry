# Overview of minikube
* A all-in-one install of Kubernetes
* Takes all the distributed components of Kubernetes and packages them into a single virtual machine to run locally
* A few (important) caveats
* Minikube will be a Kubernetes cluster running on your machine
* You will use kubectl to connect to minikube as connect to Kubernetes clusters

# Installation of kubectl, kubelet, kubeadm, kubernetes-cni in China

## Installation of kubectl - Aliyun in China
```sh
curl -Lo minikube http://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v1.0.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/

```

## Installation of minikube - Aliyun in China
```sh
curl -Lo minikube http://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v1.0.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/

```

**Recommended**:Please refer to [Here](https://github.com/HuangMarco/knowledge-hub/blob/dev/linux-operation/linux_installation_softwares_components.md#kubernates).
<br>
And also refer to [](https://yangmingxiong.com/).


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


# Resources

## Aliyun minikube

https://github.com/AliyunContainerService/minikube

## USTC Mirrors
https://mirrors.ustc.edu.cn/
<br>
https://mirrors.ustc.edu.cn/kubernetes/apt/pool/



