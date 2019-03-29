# What is kubernates

* Kubernates is the gold standard of the container orchestration
* Kubernates is developed by google and as an offshoot project named as [Borg Project](https://kubernetes.io/blog/2015/04/borg-predecessor-to-kubernetes/).
* Kubernates is the flagship project of the [Cloud Native Computing Foundation](https://www.cncf.io/).
* Kubernates is backed by many key players such as Google, AWS, Microsoft, IBM, Intel, Cisco, and RedHat.

# Main Architecture Components of Kubernates

## Cluster. 
A cluster is a set of nodes with at least one master node and several worker nodes (sometimes referred to minions) that can be virtual or physical machines.

## Kubernetes master 
The master manages the scheduling and deployment of application instances across nodes, and the full set of services the master node runs is known as the control plane. The master communicates with nodes through the Kubernetes API server. The scheduler assigns nodes to pods (one or more containers) depending on the resource and policy constraints you’ve defined.

## Kubelet
Each Kubernetes node runs an agent process called a kubelet that’s responsible for managing the state of the node: starting, stopping, and maintaining application containers based on instructions from the control plane. A kubelet receives all of its information from the Kubernetes API server.

## Pods
The basic scheduling unit, which consists of one or more containers guaranteed to be co-located on the host machine and able to share resources. Each pod is assigned a unique IP address within the cluster, allowing the application to use ports without conflict. You describe the desired state of the containers in a pod through a YAML or JSON object called a PodSpec. These objects are passed to the kubelet through the API server

## Deployments, replicas, and ReplicaSets
A deployment is a YAML object that defines the pods and the number of container instances, called replicas, for each pod. You define the number of replicas you want to have running in the cluster via a ReplicaSet, which is part of the deployment object. So, for example, if a node running a pod dies, the replica set will ensure that another pod is scheduled on another available node.


# K8S on AWS

* AWS premier container offering, Elastic Container Service (ECS), is a proprietary orchestration system - not yet k8s compatiable
* AWS has joined CNCF - it plans to support k8s in some form (ECS or new offering) is all-but-guaranteed
* k8s on AWS will be setup directly on ECS instances by hand or using kops
* kops is a tool for production grade k8s instllation, upgrades, and management - maintained by CNCF

# K8S on GCP

* GCP has high-level support for kubernates through its Google Container Engine (GKE) offering
* It is possible to use kops or manual configuration to bring-up a cluster on Google Compute Engine VMs

