# Field selector
```
前面章节提到label selector可以帮助我们查找资源。
那么field selector起到的作用类似，不同的是以下两点：
 1.通过field name来查找资源
 2.仅仅通过kubectl命令的方式来进行查找



metadata.name=my-service
metadata.namespace!=default
status.phase=Pending




kubectl get pods --field-selector status.phase=Running
上面通过kubectl命令，获取到所有status.phase为Running的Pods


kubectl get pods
kubectl get pods --field-selector ""
上面这2个是等效的，如果不指定field，那么就等于查找所有
```



## 搜索格式、
```
支持通过metadata.name和metadata.namespace的方式来搜索field

```

## 搜索的表达式
```
=, ==, and !=
其中=和双等于 是等效的
```

## 多重搜索
```
kubectl get pods --field-selector=status.phase!=Running,spec.restartPolicy=Always
通过逗号分隔多个查询表达式
```