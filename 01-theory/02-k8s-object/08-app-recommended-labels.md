# best practices for app name
```
官方给出了最佳实践，即怎样给app起label
https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/



apiVersion: apps/v1
kind: StatefulSet
metadata:
  labels:
    app.kubernetes.io/name: mysql
    app.kubernetes.io/instance: wordpress-abcxzy
    app.kubernetes.io/version: "5.7.21"
    app.kubernetes.io/component: database
    app.kubernetes.io/part-of: wordpress
    app.kubernetes.io/managed-by: helm

注意上面：name为mysql,同时instance为wordpress-abcxzy，使得应用和应用的实例区分开来

```