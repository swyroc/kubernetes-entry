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







