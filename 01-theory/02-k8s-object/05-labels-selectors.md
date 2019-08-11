# Labels
```
何为labels？ 记住了其实就是用来定义metadata元数据的东西

1.其实就是key-values键值对。
2.键值对attach到了ks object之上。
3.可以在创建的时候即被附着到object上，也可以在后面随时更改
4.当你想表述某些属性或者值的时候就使用Labels
5.持续更改的东西应当使用labels，而那些不会再变动的应当使用annotations：https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/
6.在同一个配置文件中：要求label的key必须唯一，不同配置文件中，label可以相同
7.一般都放在配置文件中，表现形式为  key:value
8.一般key由两段落组成，第一为prefix前缀，第二位name，一般previx可省略，省略的时候表示为用户私有
    如果prefix定义了，那必须是一个DNS subdomain，不允许超过253字符
    prefix与name之间以/相连
    name不能超过63个字符
    以阿拉伯字符开头，允许-_.
    系统组件比如kube-scheduler,kube-controller-manager等以及其他第三方必须加前缀
    kubernetes.io/和k8s.io/是官方预留前缀



```

## 优点
```
1.将用户的一些组织结构的定义和系统对象以松耦合的方式关联起来。其实说白了就是用户怎样给那些创建的对象命名，既方便又不是高耦合，
    同时不引入第三方，增加耦合度。（都是吹）
```

# Label selector
```
Label不确保唯一性，这个与name/uuid是不同的。
且官方都说了，他们期望很多的对象共用同样的label，不反对不同对象起相同名字
通过标签选择器，用户可以利用这个功能定义大量的对象。

当前API支持两种选择器来进行资源查找：基于等式的；基于集合的
一个标签选择器可以由多个以逗号分割的需求来组成。逗号就相当于逻辑与

```

## 基于等式的标签选择器
```
environment == production
environment = production
tier != frontend
```




```
标签选择器将筛选所有的key为environment,value为production的资源。
筛选所有key为tier，但是value不为frontend的资源，同时那些label的key不为tier的资源。这点要注意小心了。

有且只支持=， ==, !=三种类型的判断

```

## 基于集合的标签选择器
```
environment in (production, qa)
tier notin (frontend, backend)
partition
!partition
```


```
筛选所有的key为production,和所有的Key为qa的资源
筛选所有key不为fronted和backend的资源，以及所有label的key不为tier的资源，注意要小心了
筛选所有资源，满足条件为：label中的key为partition的。只要key满足条件即可
筛选的和上面的第三个相反
```




# API request url中引入label selector
```
在某些API中，在API的URL中可能会使用到Label。
比如LIST, watch API就通过label selector来筛选一些object。筛选的条件写在request URL中

equality-based requirements: ?labelSelector=environment%3Dproduction,tier%3Dfrontend
set-based requirements: ?labelSelector=environment+in+%28production%2Cqa%29%2Ctier+in+%28frontend%29

```

# REST Client中使用label selector
```
kubectl get pods -l environment=production,tier=frontend

kubectl get pods -l 'environment in (production),tier in (frontend)'


kubectl get pods -l 'environment in (production, qa)'

kubectl get pods -l 'environment,environment notin (frontend)'


```




# Service和ReplicationController
```
注意：但凡出现selector字眼的，都是使用了label selector的
service使用label selector
    "selector": {
    "component" : "redis",
    }
replicationcontroller
    selector:
        component: redis

这些都是定义在json或者yaml文件中
```



# 支持集合查询的label selector的组件
```

Job, Deployment, Replica Set, and Daemon Set都是只支持集合查询

selector:
  matchLabels:
    component: redis
  matchExpressions:
    - {key: tier, operator: In, values: [cache]}
    - {key: environment, operator: NotIn, values: [dev]}
```




