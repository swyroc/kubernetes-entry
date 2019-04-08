
# What is Kubernetes

* Kubernetes is the gold standard of the container orchestration
* Kubernetes is developed by google and as an offshoot project named as [Borg Project](https://kubernetes.io/blog/2015/04/borg-predecessor-to-kubernetes/).
* Kubernetes is the flagship project of the [Cloud Native Computing Foundation](https://www.cncf.io/).
* Kubernetes is backed by many key players such as Google, AWS, Microsoft, IBM, Intel, Cisco, and RedHat.

# Main Architecture Components of Kubernetes

Before you look into some concepts of Kubernetes, you need to realize that: the components of Kubernetes always mixed with some other concepts such as hardware concepts. For example, _the master manages the scheduling and deployment across nodes_, the master is the concept of Kubernetes components, meanwhile nodes is the Kubernetes hardware concept.

## Cluster. 
A cluster is a set of nodes with at least one master node and several worker nodes (sometimes referred to minions) that can be virtual or physical machines.

## Kubernetes master 
The master manages the scheduling and deployment of application instances across nodes, and the full set of services the master node runs is known as the control plane. The master communicates with nodes through the Kubernetes API server. The scheduler assigns nodes to pods (one or more containers) depending on the resource and policy constraints you’ve defined.

## Kubelet
Each Kubernetes node runs an agent process called a kubelet that’s responsible for managing the state of the node: starting, stopping, and maintaining application containers based on instructions from the control plane. A kubelet receives all of its information from the Kubernetes API server.

## Pods
**The basic scheduling unit**, which consists of **one or more containers** guaranteed to be co-located on the host machine and able to share resources. Each pod is assigned a unique IP address within the cluster, allowing the application to use ports without conflict. You describe the desired state of the containers in a pod through a YAML or JSON object called a PodSpec. These objects are passed to the kubelet through the API server.
<br>
Kubernetes has some unique features and one of them is that it doesn’t run the containers directly. It rather wraps up one or more containers into a pod. The concept of a pod is that any containers within the same pod use the same resources and the same local network.

The benefit is that the containers can communicate with each other easily. They are isolated but are readily available for communication.

The pods can replicate in Kubernetes. For example, an application becomes popular and a single pod isn’t able to sustain the load. At that moment, Kubernetes can be configured for deploying new replicas of the pod as per the requirement.

But it is not necessary that replication occurs only during heavy load. A pod can replicate during normal conditions as well. This helps in uniform load balancing and resisting failures.

![Kubernetes-pods](https://github.com/HuangMarco/Kubernetes-entry/blob/dev/z_Resources/images/Kubernetes-Pods.jpg)

## Deployments, replicas, and ReplicaSets
A deployment is a YAML object that defines the pods and the number of container instances, called replicas, for each pod. You define the number of replicas you want to have running in the cluster via a ReplicaSet, which is part of the deployment object. So, for example, if a node running a pod dies, the replica set will ensure that another pod is scheduled on another available node.

![Kubernetes-deployments](https://github.com/HuangMarco/Kubernetes-entry/blob/dev/z_Resources/images/Kubernetes-deployment.png)

## Overall Structure

![Kubernetes-components](https://github.com/HuangMarco/Kubernetes-entry/blob/dev/z_Resources/images/Kubernetes-components.jpg)


# Kubernetes Hardware
There are different types of hardware required for Kubernetes. Understand one thing that Kubernetes itself doesn’t need hardware, but the functioning system needs all the hardware.

## Nodes
Node is the smallest units of computing in Kubernetes. It is a singular machine and resides in a cluster. Node doesn’t necessarily need to be a physical machine or a part of the hardware. It is either a physical machine or a virtual machine. For the data center, a node is a physical machine. Similarly, for Google Cloud Platform, a node is a virtual machine. For now, we are discussing the hardware of Kubernetes. So let us consider it accordingly. But don’t limit a node as the “hardware part”. In fact, we can simply view each machine as a set of CPU and RAM resources. These machines are in a cluster and their resources can be used as per the requirement. 

![Kubernetes-node](https://www.level-up.one/wp-content/uploads/2018/07/1-3.png).

## Cluster
Nodes are appear to be small and cute processing units. we dont need to worry about the state of individual nodes because node are a part of the cluster. Also, a cluster is a collection of multiple nodes. All the nodes pool together their resources and together make a powerful machine.  When the programs are deployed onto the cluster, it dynamically handles the distribution. In short, it assigns tasks to individual nodes. In between the process, if any node is added or removed, the cluster shifts the work as per the need. The programmer need not concentrate on such things like which individual machine is running the code, etc. 

![Kubernetes-cluster](https://www.level-up.one/wp-content/uploads/2018/07/module_02_first_app.png).


## The Persistent Volumes
The programs run on the cluster and are powered by the nodes. But they don’t run on specific nodes. The programs run dynamically. Thus, there is a need for storing the information and it can’t be stored randomly in any file system. Why? For example, a program saves the data to a file. But later on, the program is relocated to another node. Next time when the program needs the file, it won’t be at the expected place. The location address is changed. To solve this problem, the traditional local storage related to each node is considered as a temporary cache for holding programs. But any locally saved data can’t be expected to persist.

# Kubernetes Software
## Containers
In Kubernetes, Linux containers host the programs. These containers are globally accepted and already have pre-built images. The images can be deployed on Kubernetes. Do you know what is containerization? It allows you to create Linux execution environments.

The programs, as well as its dependencies, are packed in one single file and shared on the internet. So anyone can download the container and deploy it on their infrastructure as per the requirement. Deployment is hassle-free with just a little setup. A container can be created with the help of a program. This enables the formation of effective CI and CD pipelines.

The containers are capable of handling multiple programs. But it is recommended to limit one process per container because it helps in troubleshooting. Updating the containers is easy and the deployment is easy if it is small. It is better to have many small containers, rather than a big one.


# K8S on AWS

* AWS premier container offering, Elastic Container Service (ECS), is a proprietary orchestration system - not yet k8s compatiable
* AWS has joined CNCF - it plans to support k8s in some form (ECS or new offering) is all-but-guaranteed
* k8s on AWS will be setup directly on ECS instances by hand or using kops
* kops is a tool for production grade k8s instllation, upgrades, and management - maintained by CNCF

# K8S on GCP

* GCP has high-level support for Kubernetes through its Google Container Engine (GKE) offering
* It is possible to use kops or manual configuration to bring-up a cluster on Google Compute Engine VMs

# Reference Links
https://www.level-up.one/kubernetes-bible-beginners/
<br>

