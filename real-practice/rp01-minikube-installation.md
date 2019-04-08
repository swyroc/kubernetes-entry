# Overview of minikube
* A all-in-one install of Kubernetes
* Takes all the distributed components of Kubernetes and packages them into a single virtual machine to run locally
* A few (important) caveats
* Minikube will be a Kubernetes cluster running on your machine
* You will use kubectl to connect to minikube as connect to Kubernetes clusters



# Installation of kubectl

## Download the latest package for OS
Here I used CentOS.

```sh
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

# change modification
chmod +x kubectl

# copy to the path
mv kubectl /usr/local/bin/kubectl

# print the kubectl version
kubectl version

```

For more detail of the kubectl installation, please refer to [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/).


# Installation of minikube
## Download the latest package for your OS
Here I used CentOS.

```sh
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube

# move minikube to the path
mv minikube /usr/local/bin/minikube
# check the version
minikube version
```

For more detail of the minikube installation, please refer to [here](https://kubernetes.io/docs/tasks/tools/install-minikube/).