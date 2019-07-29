# 粗糙理解K8S Object
```
K8S Object在K8S中是持久化对象 - 这点非常重要
KS用这些对象来表示当前集群的状态 - 这很好理解，毕竟都是数据
这些对象用来描述什么呢？
    哪些容器化手段运行的应用
    应用运行在哪些node上
    应用可使用的哪些资源
    应用的一些策略，比如重启策略，升级策略等

通过上面可以发现，K8S这样设计说到底还是为应用服务，所有一切都是围绕应用来的。
一旦你创建了一个对象，那么K8S就认死理到底了，拼到底也要为你维护住你期望的这个对象的状态
那么问题来了，你该如何使用K8S的对象呢？
    通过K8S API来使用它的对象，当然你可能不会直接触碰到这些API，比如你可以在虚机中通过kubectl这个command line 
    interface，通过敲命令的方式来调用K8S API
    亦或者你可以通过K8S为你提供的类库来调用K8S API
```

# Object Spec和Object Status
```
从高层架构来理解K8S对象的话，那么K8S对象可以分为两大部分：
    object specification
    object status
K8S的世界充斥着数据，而理想和现实总是有差距的，那么前者就是理想，后者就是现实
K8S竭力为你实现理想，但是难保现实中不存在落差
```

## Object Specification
```
注意哈，你必须提供Object spec，它被用来描述你要创建的这个K8S对象的期望属性

更多的想要去理解object specifiacation，那么访问：
https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md
这里面用来表述你可以为你的object specification定义哪些K8S能够识别的元数据
```

## Object Stauts
```
object status表示真实场景下，K8S为你创建的对象的真实状态。
```
