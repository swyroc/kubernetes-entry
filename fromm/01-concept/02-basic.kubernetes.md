# 浅谈K8S Object
K8S本质上是一个集群，K8S是一种容器编排系统，而其容器编排的对象是POD。而POD是K8S的API Server支持的众多资源类型中的其中一种。

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













