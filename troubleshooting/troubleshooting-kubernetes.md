# What is it?
This is the summary of the troubleshooting part.

# ImagePullBackOff - kubectl deployment
```sh
kubectl expose deployment hello-minikube --type=NodePort
kubectl get pod
kubectl desribe pod <pod name here>

```
After you execute above command, if the status of the pod is **ImagePullBackOff**, the possible reasons can be below:

* Wrong container Image/Invalid Registry permission

Start a single instance of nginx.
  kubectl run nginx --image=nginx
For detail you can access [here](https://kukulinski.com/10-most-common-reasons-kubernetes-deployments-fail-part-1/).

# CrashLoopBackOff -kubectl run
_CrashLoopBackOff_ tells us that Kuberenetes is trying to launch this Pod, but one or more of the containers is crashing or getting killed.

```sh
kubectl logs <pod name here>

```