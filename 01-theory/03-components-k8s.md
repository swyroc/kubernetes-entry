# 组件

## 主组件


所谓主组件，就是提供控制功能的主面板组件。官网上的重点圈出来就是：Master components provide the cluster’s **control plane**.
```
主组件顾名思义，就是提供控制管理功能。
针对于任何集群cluster的event做出响应
为了更好的管理，主组件最好安装在同一台机器上

```

### kube-apiserver
```
如果K8S要对外提供服务，得想办法啊，所以就有了kube-apiserver
负责对外暴露kubernetes API
对于K8S的控制面板来说，它属于前端

```

### etcd
```
K8S,再怎么弄也是一堆数据，在K8S中，一切也是对象，都需要被存储起来。
etcd是key-value键值对的存储数据库，负责存储所有的集群相关的数据
如果决定使用etcd作为后端存储的数据库，就必须要有备份计划：
https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster
更多关于etcd，参照：
https://etcd.io/docs/

```

### kube-scheduler
```
主要负责进行调度选举哪个node来运行pod，将调度出来的结果转交给kube-controller-manager来安排运行
其本身不负责任何的其他实际操作
```

### kube-controller-manager
```
负责运行controller的主组件
逻辑上，controller是一个个的进程，但是真实环境下，所有的控制器都被编译到一个二进制包，然后用一个单独的进程运行

```

#### controller
```
控制器分为以下种类：
    Node Controller - 负责提醒或者响应，当天node挂掉的时候
    Replication Controller - 负责为每一个RC维护目标数量的pods
    Endpoints Controller - 负责维护Endpoints对象，比如Service, Pods等
    Service Account & Token Controller - 为新的命名空间创建默认账户和API access token
```

## Node 组件
相对于主组件，就有了Node组件，其实就是真正干事情的组件
```
Node组件运行在每个node上，负责维护pod，以及提供k8s运行时环境
```

### kubelet
```
就是一个代理，在每个node上必定有一个kubelet
用于保证定制好的容器都运行在container上
kubelet拿着一大堆PodSpecs,这些PodSpecs里面放的是什么呢，放的是期望创建的container的描述。
然后Kubelet根据这些描述去创建期望的containers
```

### kube-proxy
```
在集群中的每一个Node上都有一个kube-proxy
主要负责：
    管理k8s的service的网络规则
    负责connection forwarding，其中主要负责请求跳转request forwarding。
    允许TCP和UDP
    基于算法round robin来在一系列的后端服务中进行转发
```

### container runtime
```
其实就是真正负责运行container的组件，比如docker, containerd, cri-o, rklet等.
但是不是说，只要是个container runtime就可以了，这些组件的前提条件就是实现k8s的容器接口：
Kubernetes CRI (Container Runtime Interface): 
    https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md
```

## 插件Addons


### DNS
```
虽然不是强制性的，但是大多数的K8S的集群都使用cluster DNS，很多都依赖于它
Cluster DNS是一个DNS server，为K8S维护内部service的DNS
K8S的容器启动的时候默认自动包含了dns server

https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/


```

### Web UI Dashboard
```
web-based UI，为K8S集群服务。通过在UI界面对K8S的集群的资源进行操作
https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
```


### Container Resource Monitoring
```
基于时间序列来存储container的状态，并且提供一个UI界面来浏览相应数据。所有这些数据集中保存在中心数据库
https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/
```

### Cluster-level Logging
```
负责将容器日志集中存储在在一个central log store里。同时对外提供search/browsing接口
https://kubernetes.io/docs/concepts/cluster-administration/logging/
```




