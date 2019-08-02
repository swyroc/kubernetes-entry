# Names
```
K8S做了很多类似这样的事情，比如怎样标识不同的API，为此引入了Name和GUID。
K8S争取将每个事物都标明成一个对象，哪怕API都不放过。真是凶残。

同时为此制订了一些规则：
    同一时间，同样Name的API对象只能同时存在一个
    最大长度不允许超过253个字符
    只能由小写的阿拉伯字符，-和.组成
    但是其他资源相关的可能有更多其他限制
以下是例子：
    apiVersion: v1
    kind: Pod
    metadata:
    name: nginx-demo
    spec:
    containers:
    - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

# UIDs
```
每个K8S创建的对象都有唯一一个K8S为其创建并分配的字符串，用来唯一标示该对象。

```