# What is it
This is a common exercise to deploy the tomcat app server by using the official docker iamge.

# Gemeral Steps
* Define the deployment
* Expose the tomcat services
* Deploy the app server to Kubernetes cluster


# Define the deployment
**Deployment** should and must be described as a configuration file using YAML format. The most most simple deployment is just a single Pod. A Pod is an instance of container which is a logical concept. Deployment can has any number of Pods as you wish.

## First deployment yaml
Create a new yaml and named as _deployment.yml_, you can just copy the content of [rp03-deployment.yml](https://github.com/HuangMarco/kubernetes-entry/blob/dev/02-real-practice/rp03-deployment.yml).

