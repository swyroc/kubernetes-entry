# 浅谈K8S Object
K8S本质上是一个集群，K8S是一种容器编排系统，而其容器编排的对象是POD。而POD是K8S的API Server支持的众多资源类型中的其中一种。
<br>
容器是什么，其实就是应用程序。K8S其实可以被看作一种接口，接口隐藏了底层的实现细节，而接口功能让用户可以增删改查**容器**。更进一步的说，增删改查的对象是**POD**，而运行POD的目的就是在POD中运行容器。通过POD就可以把容器创建并运行起来了。但是随之带来多个问题：
* POD如何对外提供服务？也就是POD里面的容器提供的服务如何让外部的客户端所访问？
* 万一POD发生故障并崩溃，怎么办？

容器编排系统必须具备的就是自动恢复，保证高可用，而POD自身是不具备自动恢复功能的。K8S通过POD Controller来支持刚刚所说的自动恢复等功能的。最著名的Controller就是Deployment资源类型对象，既是资源也是类型也是对象。创建Deployment来控制指挥创建多少个POD。而具体创建多少个POD等，取决于用户的定义。
<br>
总结一下说的更加直白点：用户并不会直接创建POD，而是用户通过创建Deployment来控制创建多少个POD。


# K8S Resources
## K8S支持的基本资源对象。
### POD

### Service

### Namespace

### Volume

## 基础对象之上的高级资源类型

### Controller
* ReplicaSet
* Deployment
* DaemonSet
* StatefulSet
* JOB

# 动态服务
当POD发生故障的时候，那么K8S的总体策略是多退少补，发生故障的POD将会被一个新创建的POD所替代，而此时的POD的IP地址很大可能与之前的POD的IP地址不同，假设之前有一个客户端访问的POD的IP地址为10.21.1.122,那么当该提供服务的POD挂掉之后，K8S创建了新的POD，而新的POD的IP地址不再是之前的IP地址，那么此时客户端将无法正常访问之前的服务，那么如果这种事情发生是与容器编排的精神所违背的。动态逻辑上为了实现客户端与服务端之间的交互，就引入了新的解决方案：服务注册和服务发现，通过这种方式来实现服务的衔接。在我们提到的这个场景下，POD是动态创建以及销毁的，那么很显然我们就需要引入到服务注册和服务发现来解决POD崩掉重新新建POD同时客户端依然能够正常访问的问题，即动态服务的衔接。
<br>
## Service层
在K8S中是借助于DNS组件来完成服务注册与服务发现的。然而DNS解析的结果不是POD，因为POD和客户端之间还有一service层。意思就是：客户端直接访问的并不是POD，而是直接访问固定接口service层，该层固定提供给客户端访问。
* 每当新建一个新的POD对外提供服务的时候，应当首先在POD之前添加一个新的service层作为中间层
* 不管POD IP怎么变化，service层采用域名访问
* Service层也作为一种资源
* Service层被创建的时候一定会具备名称即domain name
* Service将用户的请求转发至POD
* Service可以被看作是POD的反向代理，同时也可被看做是调度器
* Service在被创建完成之后也会有自己的地址被称为service IP或者cluster IP，只要不删除service，那么service IP不会变。POD也有自己的IP被称为POD IP

Service在代理POD的时候也会发生POD ip地址改变的情况，那么service如何发现要代理的POD的IP地址发生改变呢？即将引入K8S极具创意的解决方案:
<br>
K8S为每一个资源对象都附加了一个标签。K8S通过标签来引用资源。而不再是使用IP地址。标签就可以被看作是键值。service层为POD做反向代理的时候，不是通过POD IP地址来关联而是通过label即标签来进行关联。

### label selector
service通过label selector即标签选择器来有选择性的调度或者反向代理特定的POD。label selector拥有过滤选择器来过滤掉不需要的标签。比如当前有2个POD运行Nginx，两个POD都有label为app:nginx，当其中一台挂掉了系统自动重新创建了新的nginx容器同时为该容器打上原来的标签，因此即便IP地址变更，但是label是不会变更的。那么service层通过标签选择器就能够自动获取到重新创建的Nginx容器，从而更进一步获取到期望的POD IP地址。

## DNS
上面提到只要service层不被删除重建，那么Service层的IP地址就不会发生改变，那么肯定是存在情况service被删除的情况，那么一旦被删除，service IP地址也会发生改变，那么我们之前提到的问题依然会发生，那怎样解决service 层IP地址变更的问题呢？
<br>
K8S引入了DNS组件。
* 功能是动态的
* K8S将创建的service IP地址与service name之间的对应关系作为一条A记录动态的注册到DNS中
* 客户端只要请求DNS中的service name，就一定能够找到对应的IP地址
* 即便Service层重建，K8S依然能够通过DNS精确精准的找到对应的IP地址
* 客户端需要去插座特定的服务的时候，只需要向DNS请求服务名称，那么就能够自动获取到服务对应的IP地址。
* 从此以后客户端要访问的不是service层的IP，而是service层的名称

### 什么是客户端
nmt
* n - nginx的客户端，表示远程客户端，即发起请求的客户端
* t - nginx
* m - t的的程序

比如拿nmt即：nginx, mysql, tomcat三者来说，nginx的客户端是用户的浏览器，是远程的客户端，t的客户端是nginx，因为nginx要向tomcat发生访问。mysql的客户端是运行在tomcat上的应用程序。
<br>
在K8S上的设计：
* nginx不能直接访问tomcat，而是应当在tomcat与nginx之间添加一个新的service层，nginx直接访问service层
* service层转发请求到tomcat
* tomcat访问mysql的service层，mysql service层将请求转发至mysql
* nginx控制器来管理nginx pod
* tomcat控制器来管理tomcat pod
* mysql控制器来管理mysql pod
* 客户端也不会直接到达nginx，而是先到达nginx的service层

**所以从上面看，使用K8S已经完完全全带来了整体操作方式的改变。需要从资源设计收集入手，去规划大致一个集群需要多少资源**。这点非常重要！从上会得出即将产生9个资源：
* 3个控制器 - 由用户直接创建
* 3个service层 - 由用户直接创建
* 3个pod 由控制器创建，非我们直接创建

所以由此产生一个非常重要的思想：当架构迁移到K8S上的时候，考虑的习惯和设计和以往传统的思维大相径庭，需要从一开始就映射到K8S的组件，需要计算需要多少层，多少控制器多少资源等等等等。
* 控制器将会成为运维发布以及变更的重要组件，控制器负责POD的部署创建、扩容变更、故障处理重建
* 控制器自动完成，控制器封装了运维人员运维操作的内容，所以控制器可以替代运维人员，但是仅仅针对于静态内容管理


# Kubernetes Network
![Kubernetes Network](https://github.com/HuangMarco/Kubernetes-entry/blob/dev/z_Resources/images/kubernetes-network.jpg)

* 节点与节点之间有节点网络，节点有自己的IP地址，通过IP进行通信
* 每个Node内的各个POD之间有POD网络，POD和POD通过POD IP通信
* Service网络
* Node01中的POD要访问Node02中的POD需要跨越2个网络：Service网络和POD网络



# 涉及到的部署工具以及一些概念
* kubeadm
* kops
* kubespray
* kontena Pharos

## 二次封装的常用发行版
* Rancher - Rancher Labs二次发行的K8S
* Tectonic - CoreOS二次发行的K8S
* Openshift - 需要首先会ansible，是红帽子公司基于K8S的二次发行版，将不成熟部分隔离，只保留K8S成熟部分。

上面最著名的是Rancher和Openshift.后者是美籍华人创建的容器编排系统。目前来说绝大部分的公司使用的都是K8S的原始版。


# K8S的部署方式
K8S有两种部署方式,两种运行逻辑：

![Kubernetes Deployment](https://github.com/HuangMarco/Kubernetes-entry/blob/dev/z_Resources/images/kubernetes-deployment-01.jpg)

上图中，每个关键组件都运行为守护进程。如果是守护进程，那么master上是不需要有kubelet以及docker的。只有容器才需要kubelet,docker。最上面的是addons。

![Kubernetes Deployment 02](https://github.com/HuangMarco/Kubernetes-entry/blob/dev/z_Resources/images/kubernetes-deployment-02.jpg)

上图表示每个组件都运行为容器。且master和node都有相同的Kubelet以及docker组件。kubeadm是以第二种方式运行的，master上的组件都要运行为pod，node上的组件也都要运行为pod。而在底层都要以Kubelet以及docker运行容器。既然第二种部署方式是以POD形式来运行的，那么要运行POD就需要镜像image，那么从哪里获取到相应的image就是一个难题。这些镜像都在gcr.io上。即可google container registry。该网站在国内是无法访问的。K8S的安装由于国内无法访问gcr.io。

<br>

* 使用Kubeadm以第二种方式部署运行K8S，那么由于国内无法访问gcr.io，导致各个组件POD的镜像无法被下载。需要使用某种方式拿到下载好的镜像
* Kublet镜像阿里已经开放入口获取
* 先安装kubelet，然后才能安装kubeadm，安装好kubeadm之后，然后才能以容器化的方式运行POD，从而部署好整个集群














