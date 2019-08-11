# node
```
在KS中就是干活的。也被称为minion。
1.根据集群不同，既能是VM也能是一个物理机。
2.每个node上面被部署服务来运行pod
3.被master管理，真特么悲剧

更多细节：
https://git.k8s.io/community/contributors/design-proposals/architecture/architecture.md#the-kubernetes-node

运行在node上面的服务：
1.包含container runtime
2.kubelet
3.kube-proxy


```

## Node的3个方面
```
官网首先抛出一个命令：

kubectl describe node <insert-node-name-here>
通过上面命令可以查看这个node的一些信息

1.addresses - 地址
2.condition - 当前的一些状态
3.Capacity and Allocatable - 容量以及分配的情况
4.Info -  其他的一些版本信息

```




### addresses
```
有哪些呢？
1.hostname主机名
2.externalIP对外的IP地址
3.interalIP对内的IP地址

也就是说，node的地址是包含上面3个部分的。
其中hostname是node内核负责声明的，可以通过命令kubelet --hostname-override更改
外部IP可以在集群外部通过该IP被访问到
内部IP只有在集群内部使用
```


### conditions
```
描述所有running node的信息，不running没人鸟你

https://kubernetes.io/docs/concepts/architecture/nodes/#condition

那么ks为node定义了哪些conditions类型的字段呢？
OutOfDisk
Ready
MemoryPressure
PIDPressure
DiskPressure
NetworkUnavailable

注意哈，这里有点绕，首先node conditions类型的字段有很多，可以把不同字段想象成不同维度
那么把重要的关注点抽取出来，以Ready类型的conditions字段为例：

大致像下面这样：
"conditions": [
  {
    "type": "Ready",
    "status": "True",
    "reason": "KubeletReady",
    "message": "kubelet is posting ready status",
    "lastHeartbeatTime": "2019-06-05T18:38:35Z",
    "lastTransitionTime": "2019-06-05T11:41:27Z"
  }
]

可以看到上面的conditions为json数组，上面例子只包含了一个Ready类型的，其实还可以放很多其他类型的。

```
