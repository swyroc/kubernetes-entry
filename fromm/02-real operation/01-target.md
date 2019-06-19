# 实战目标
* K8S版本 - kubernetes 1.13.1
* 搭建K8S集群，集群中master节点和node节点数量可控
* 通过kubeadm搭建集群，通过kubeadm部署那么需要2个程序包，一个是kubeadm,一个是kubelet。


# 参照文档
穿第一手鞋，那么我们需要通过Kubernetes官网来一步步的完成kubernetes集群的搭建。这里不再是Minikube测试环境，而是直接上真实的产品环境。
https://kubernetes.io/docs/setup/
<br>
另外附上https://www.jianshu.com/p/9e730795c199
同时注意旁边这个链接里面的涉及到docker的就是一坨狗屎，是错的，亲测。其他的从阿里云上下载的，是对的，亲测。


# 安装
## Docker安装
```sh
直接参照https://github.com/HuangMarco/knowledge-hub/blob/dev/os/linux-operation/linux_installation_softwares_components.md#install-docker-ce---ubuntu
速度杠杠滴
```

## 添加阿里云的kubernetes apt-key
```sh
sudo apt update && sudo apt install -y apt-transport-https curl
curl -s https://mirrors.aliyun.com/kubernetes/apt/doc/apt-key.gpg | sudo apt-key add -
```

## 添加Kubernetes源
```sh
sudo vim /etc/apt/sources.list.d/kubernetes.list
# 添加如下源
deb https://mirrors.aliyun.com/kubernetes/apt/ kubernetes-xenial main

```

## 开始下载安装kubeadm，kubelet, kubectl
在公司防火墙内部不确定可行不可行哈
```sh

sudo apt update
sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
好，至此安装结束了。


# 初始化

## 初始化Master节点


