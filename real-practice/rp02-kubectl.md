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
    <br>Notice: The file should be yaml or json format.


* flags - Specifies optional flags.

```sh

kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080

kubectl expose deployment hello-minikube --type=NodePort

```