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


#### 时间同步
因为是Ubuntu系统，所以这里不再进行任何的时间同步。

#### 各个节点主机名称解析
```sh
vi /etc/hosts

# 添加以下内容：
# <master IP 地址> master.hk.com master
# <node 1 IP 地址> node01.hk.com node01
# <node 2 IP 地址> node02.hk.com node02
# <node 3 IP 地址> node03.hk.com node03

nslookup node01.hk.com 

```

注意：需要为各个节点同步相同的信息在/etc/hosts文件中。



#### 关闭iptables和firewalld
```sh
systemctl status firewalld
systemctl status iptables


systemctl stop firewalld.service
systemctl stop iptables.service
systemctl disable firewalld.service
systemctl disable iptables.service
```

#### 禁用SELinux
```sh
getenforce

vi /etc/selinux/config # 从enforcing改为disabled
# vi /ect/sysconfig/selinux/config

```
要确保每个节点的SELinux都处于关闭状态。

#### 关闭swap
```sh
free -m # 可以查看swap space

swapoff -a # 禁用swap设备，关闭所有swap设备，只是临时有效。

vi /etc/fstab #注释掉所有swap类型的设备

```

#### 启用ipvs内核模块

```sh
cd /usr/lib/modules/kernal/net/netfilter/ipvs
可以看到上面的这个目录下包含了很多其他的文件。

```


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

### docker服务的配置
**要注意：**Kubernetes使用docker存在几个问题：
* docker安装本身并没有配置文件，需要手动添加配置文件daemon.json
* docker要使用加速服务
* docker的默认的某些配置必须要更改
* docker的某些镜像在国内是访问不到的，所以要相应做一些修改

#### 更改docker.service配置项
```
1. docker镜像要启动加速服务

2. docker默认启动之后会将iptables的默认策略从FARWARD改为DROP，而此行为会影响K8S的集群依赖的报文转发功能。因此需要在docker服务启动之后，
重新将FORWARD链默认策略改回ACCEPT。

3. 默认情况下kubernetes中docker去启动POD时用到的几个镜像会通过默认的k8s.gcr.io去获取。但是默认国内是无法访问k8s.gcr.io的。
如果要通过默认的k8s.gcr.io镜像仓库获取Kubernetes系统组件的相关镜像，需要配置docker Unit File (Ubuntu下/lib/systemd/system/docker.service，CentOS为/usr/lib/systemd/system/docker.service)中的
Environment环境变量，为其定义适用的HTTPS_PROXY，指定一个服务器让我们跳转以便去访问k8s.gcr.io

备注：个人对上面第三点比较怀疑，因为在本地实际测试，docker login是可以成功的，所以案例就是在某些情况下当你的网络受到限制的时候，你确实是需要做一些设置以便让你成功的登陆docker>
比如你再某些公司网段，而公司内部限制了对于docker hub的访问权限，那么你确实是无法访问到docker hub，以及docker login的。那么此时你就需要采用上面的某些方式，比如架设代理服务器，代理服务器可以访问docker hub，或者docker registry。

可以：https://www.cnblogs.com/atuotuo/p/7298673.html
https://www.cnblogs.com/zhangmingcheng/p/7084836.html

但是在家里的电脑上完全没有必要这样。可以直接诶docker login，国内没有禁掉该功能。

更多功能要访问：

4. 因为上面用到了代理，那么一旦你配制了代理，但是当K8S去访问本地的网络的情况下是没有必要配置代理的，那么我们需要将本地网络排除在外。

vi /lib/systemd/system/docker.service

# Add below:

ExecStartPost=/usr/sbin/iptables -P FORWARD ACCEPT




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


