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

## view pod log
```sh
kubectl logs <your pod name>

```
### get the log that are updating in the real time
```sh
kubectl logs -f <your pod name>
```

## exec command to run an interactive show inside the model of pod
This command was used to troubleshoot within the container.

```sh
kubectl exec <your pod name> --stdin --tty -c <your pod name> /bin/sh
# Continueously you will type some other shell commands to do the troubleshooting
$: ping ...
$: exit # use exit to logout from the troubleshooting
```




