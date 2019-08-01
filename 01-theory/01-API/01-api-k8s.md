# K8S API
```
https://kubernetes.io/docs/concepts/overview/kubernetes-api/

类似于odata，为什么K8S也要搞这种API版本。即不同版本的API从路径上就可以看出来。
你以后会经常看到类似于/api/v1,/apis/extensions/v1beta1等奇怪的API。

Different API versions imply different levels of stability and support.

也就是说K8S官方认为：一个成功的产品离不开对新特性的支持，总之要时刻保持新高度去装逼
那么由此K8S在API的版本上分为了后面我即将要说的一些版本。
```

## Alpha level
```
请求的API中包含alpha字样
裸奔中，可能会有Bug,默认就禁掉了
见异思迁，今天支持，明天可能突然不支持了
神不知鬼不觉，可能API的内容在下一版本就变了

```

## Beta level
```
请求的API中包含beta，例如v2beta3
API是被良好测试过的，默认是安全的，默认是开启的
K8S会一直支持下去，但是内容可能会变更
因为是BETA版本嘛，所以很多东西可能还是会变更，建议在非商业情景下使用
但是K8S官方强烈建议大家一起使用这个版本的API，为它免费测试BUG
```

## Stable level
```
毫无疑问，正式版本
请求的API中包含vX，其中X是整形数字
永远正规
```

