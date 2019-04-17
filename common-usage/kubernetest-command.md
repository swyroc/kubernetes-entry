# kubectl

## create pod
```sh
kubectl create -f pods/<your deployment file name>.yml
```
## get all the pods
```sh
kubectl get pods
```

## describe pod
```sh
kubectl describe pods <your pod name>
```

## port forwarding
PAS allocates a private IP address by default and cannot be reached outside of the cluster. You can use _port-forward_ command to map a local port to a port inside your pod.

```sh
kubectl port-forward <your pod name> <new port number>:<your pod port number>
```