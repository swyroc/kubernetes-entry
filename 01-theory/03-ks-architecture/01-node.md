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