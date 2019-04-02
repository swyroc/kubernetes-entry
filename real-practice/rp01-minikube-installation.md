# Overview of minikube
* A all-in-one install of Kubernates
* Takes all the distributed components of Kubernates and packages them into a single virtual machine to run locally
* A few (important) caveats
* Minikube will be a Kubernates cluster running on your machine
* You will use kubectl to connect to minikube as connect to Kubernates clusters



# Installation of kubectl

## Download the latest package for OS
```sh
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

# change modification
chmod +x kubectl

# copy to the path
mv kubectl /usr/local/bin/kubectl

```

For more detail of the kubectl installation, please refer to [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/).


