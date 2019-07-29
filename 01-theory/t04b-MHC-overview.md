# What is it
MHC(Monitoring and Health Check) is a big topic within Kubernetes. Kubernetes will do the readiness check upon the Pods container. If a container is not available then it will be removed from the load balancers. Liveness probes indicate a container is alive. If aliveness fails multiple times, then the container will be restarted. 

# kubelet
Kubernetes do the aliveness via kubelet in each Kubernetes Node. Kubelet is Kubernetes daemon, and kubelet is responsible for making sure that a pod is healthy, it will perform the alive check.

# Questions for the HC
* How is the readiness probe performed
* How ofter is the readiness checked
* How ofter is the liveness probe checked

## How is the readiness probe performed
You can just have a look at healthy.yml for the answer.
```
readinessProbe:
    httpGet:
        path: /readiness
        port: 81
        scheme: HTTP
        initialDelaySeconds: 5
        timeoutSeconds: 1
```
From above we realize that: httpGet request is sent to the application along the readiness route on port 81. This happens after 5 seconds. A response between 200 and 400 must be returned and that has to happen within 1 second.

## How ofter is the readiness checked
You can use _kubectl describe pods <your healthy check name> | grep Readiness_ command for the frequency. The response looks like below:

```
Readiness:
http-get http://:81/readiness
delay=5s
timeout=1s
period=10s
```
From above we realize that _period=10s_ is the frequency we want.

## Liveness probe
You can also use _kubectl describe pods <your healthy check name> | grep Liveness_ command for the Liveness.
```
Liveness:
    http-get http://:81/healthz
    delay=5s
    timeout=5s
    period=15s
```
From above we realize that _period=15s_ is the frequency we want.


# Reference Link
Liveness:<br>
http://kubernetes.io/docs/user-guide/liveness/
