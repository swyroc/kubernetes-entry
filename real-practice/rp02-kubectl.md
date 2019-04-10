# Prerequisities
Before you start this session, you should already completed the previous session.

# Overview of kubectl
For overriew of kubectl you should visit [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/).

# kubectl command

## Basic grammar

kubectl [command] [TYPE] [NAME] [flags]

* command - For all the available commands kubectl supports you shuold visit [kubectl commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands).
* TYPE - type of the resource and case-sensitive. For all the resource type kubectl can operation you should visit [resource type](https://kubernetes.io/docs/reference/kubectl/overview/#resource-types).
 - NAME - name of the resource and case-sensitive. There are mainly three ways to use type along with name as below:<br>
    - Resource with same type: TYPE1 name1 name2 name<#>. 
    <br>Example: kubectl get pod example-pod1 example-pod2
    - Multiple resource types individually: TYPE1/name1 TYPE1/name2 TYPE2/name3 TYPE<#>/name<#>. 
    <br>Example: kubectl get pod/example-pod1 replicationcontroller/example-rc1
    - Resources with one or more files: -f file1 -f file2 -f file<#>. 
    <br>Example: kubectl get pod -f ./pod.yaml
    <br>Notice: The file should be YAML or Json format. The kubernetes official prefer to YAML more than Json.


* flags - Specifies optional flags.


## kubectl api-resources

```sh

kubectl api-resources # All the resources will display on the console

```

### Example commands

```sh
kubectl run --help

# Run a specified image hello-minikube on the cluster.

kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080


# Expose a replication controller, service, or pod as a new Kubernetes service.
kubectl expose --help

kubectl expose deployment hello-minikube --type=NodePort

kubectl get pod # you will get the service you created, here it is hello-minikube

minikube service <you service name> --url
```

## Two way to run a container

### kubectl run
```sh
kubectl run nginx --image=nginx --port=8989

```
### kubectl expose
```sh
kubectl expose deployment nginx --type=NodePort

kubectl get pod # you will get the service you created, here it is hello-minikube

minikube service <you service name> --url

```

**Notice**:No matter which way you use to create pod, at last you will find that: docker will create new image for you. E.g, you execute _kubectl expose deployment nginx --type=NodePort_ then you execute _docker images_ you will find the nginx image there.


## Delete resources
### kubectl delete <resource type>

```sh
kubectl get pod
kubectl delete pod <pod name you copy from above resule>
```

**Notice**: <br> 
* The resouce type should be exactly the same with option after _kubectl delete_. E.g, _kubectl delete pod <pod name but not service name>_ 
<br>
You need to be firstly clear with the concept of **deployment, pod, container**. If you create a pod by running _kubectl expose deployment <deployment name>_, it will not work in case you just run _kubectl delete pod <pod name>_. See below for example:
<br>

```sh
kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080

# you cannot just use kubectl delete pod, because outside there is a deployment there, even you delete the pod it will continue to create new pod

# kubectl delete deployment used to both of the two ways of running a container: kubectl run & kubectl expose

kubectl delete deployment hello-minikube

```
