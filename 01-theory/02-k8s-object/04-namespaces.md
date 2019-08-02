# Namespaces
```
K8S支持真实物理集群之上的虚拟集群。这些虚拟集群被称为命名空间namespaces

命名空间主要用来在不同的用户之间隔离集群的资源。

适用场景：
    横跨部署的环境中有很多部门的很多users，或者牵涉到很多项目。那么此时应当启用namespace>
    如果集群的用户不多，那么此时就不需要使用到集群


K8S的namespaces功能会限定你起到name的范围。比如在一个命名空间内资源的name应当唯一。但是横跨多个namespace情况下就不需要了。
不支持嵌套，且每一个k8s的资源只能定义到一个namespace中。

在未来K8S的版本中，在同一个命名空间内的对象默认将具备同样的权限控制策略。

怎样创建命名空间：https://kubernetes.io/docs/tasks/administer-cluster/namespaces/


不管是什么k8s资源，pods, services, replication controllers都是在命名空间里被管理的。
但是有些低级别低维度的资源，比如nodes,persistent volumes，并不在namespace中。


```

# 操作
```
kubectl get namespace - 列出当前在一个集群中的所有的命名空间

NAME          STATUS    AGE
default       Active    1d
kube-system   Active    1d
kube-public   Active    1d

    默认没有显式指定命名空间的对象会被默认分配一个名为default的命名空间
    默认由k8s创建的对象将被分配到名称为kube-system的命名空间
    默认会自动创建一个名称为kube-public的命名空间，这个命名空间里主要标识在整个集群中
        可见并可读的公共对象

 

```

## 设置namespace
```
如果用户通过kubectl去做某些操作，其实本质上是通过kubectl向k8s的api-server发起请求。
那么这个说到底还是一个request。
如果要对这个request进行namespace的设定,那么就会需要使用--namespace选项

    kubectl run nginx --image=nginx --namespace=<insert-namespace-name-here>
    kubectl get pods --namespace=<insert-namespace-name-here>

如果要永久性的为之后的kubectl命令设置namespace：
    kubectl config set-context --current --namespace=<insert-namespace-name-here>
    # Validate it
    kubectl config view | grep namespace:    
```

# namespace与service
```
当你创建一个service的时候，就会默认创建一条DNS记录。这条记录由以下几部分组成：
    <service-name>.<namespace-name>.svc.cluster.local
上面意味着如果一个容器使用<service-name>，那么就会默认路由到这个service
    最终肯定会链接到某个namespace上。
如果要跨namespace，那么就要使用FQDN。

```

## 哪些不在namespace
```
# In a namespace
kubectl api-resources --namespaced=true

# Not in a namespace
kubectl api-resources --namespaced=false

```