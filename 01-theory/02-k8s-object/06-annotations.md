# Annotations
```
和labels一样，都是为了用来定义元数据。
从这里面也可以看到ks做事的哲学，保留了一个通道同时预留了另外一个。
当你希望label用了又可以查到，那么使用label selector
如果你对可查性要求没那么高，仅仅希望定义元数据即可，那么使用annotations

"metadata": {
  "annotations": {
    "key1" : "value1",
    "key2" : "value2"
  }
}


其语法部分和labels相同，即prefix和name组成key。字符方面的要求也与label相似。
除了没有基于等式和基于集合可查等功能。其他都一样。
```


