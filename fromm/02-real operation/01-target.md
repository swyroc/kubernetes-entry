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

## 安装前言
整个安装大概要经历以下步骤：

### 主机环境预设
master和各个node节点的系统环境要预先设置好，满足我们的一些基本诉求。
本次实验中，准备1个主节点，2个node。

* master - 1
* node - 2

系统设置：
* 各个节点的要设定时间同步,CentOS系统的要通过NTP服务设定时间
* 内网的要通过DNS完成各个节点的主机名称解析，本次实验使用hosts文件来进行
* 关闭各个节点的iptables或者firewalld服务，确保它们被禁止随系统引导过程启动
* 各个节点禁用SELinux，如果不禁用会导致启动容器出现各种问题
* 各个节点禁用所有的Swap设备，如果在生产环境中启用swap，那么就代表生产环境内存不够用了，而启用swap看上去是能够节约系统内存，但是对系统性能的影响是极其巨大的。k8s默认禁用swap。
* 如果要使用ipvs模型的proxy，还要通过手动让各个节点载入ipvs相关的模块。service有两种类型，一种是iptables，一种是ipvs。




### 安装程序包
在master和各个Node节点上安装程序包，比如docker, kubelet, kubeadm等。


### 启动docker等服务

### 初始化master主节点


### 将各个node添加到集群中



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


