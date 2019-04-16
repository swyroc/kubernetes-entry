# kubectl run
```
Deploy an application to Kubernetes cluster, by deploying an image include the application source code to kubernetes cluster you can run an image quickly.

```

# kubectl expose
```
By running this command kubernetes will create an external load balancer with a public IP address attached to it. Any client who hits that public IP address will be routed to the pods behind the service.

```

# kubectl get services
```
By running this command we can let Kubernetes list all of the services and we can see that container with public IP to let user hit the container remotely. Kubernetes supports an easy way to use workflow out of the box using the kubectl run and expose commands.
```