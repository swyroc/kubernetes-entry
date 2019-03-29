# Container & Container Orchestration

## Differences between Container and Container Orchestration

### Notice:
* Container is the result of the application been packaged.<br>
* Container & Container Orchestration are the logical concept.
* Applications are broken up into various discrete services that packaged in container.
* The number of container and the number of application (service) are not always equal. One application could have more than one container via scaling.
* The communication between the containers of the same application is the issue. 

**Docker** is the **tool** to package the application to **build out a container**. Docker is not the container.
<br>
If you have ten containers and four applications, it’s not that difficult to manage the deployment and maintenance of your containers. If, on the other hand, you have 1,000 containers and 400 services, management gets much more complicated. 

It is not difficult to create a container for application, but when you want to scale the application from one container to multiple containers, many issues might show themselves for the scalablity. From above we realize that: **We need a tool to help us with scaling the existing multiple containers**.

<br>
Kubernates is the tool to help with container management - automating the deployment, management, scaling, networking and availability of multiple containers.
Kubernates is the container orchestration tool.

![Old Shipment](https://github.com/HuangMarco/kubernates-entry/blob/dev/z_Resources/images/old-shipment.jpg)

Before, all the goods are shipped by a boat and goods are loose and are not well organized. The unit of shipping goods is the box. After the goods are shipped to the land, worker needs to sort each goods box and classify them according to each goods box's belongling.

And now look at the modern shipment:<br>

![Old Shipment](https://github.com/HuangMarco/kubernates-entry/blob/dev/z_Resources/images/modern-shipment.jpg)

Now the goods are shipped by using container. Goods are placed into container and goods are well organized. There is a mechanism to manage all the containers. By managing containers the goods are also well managed. This is called container orchestration. If one container cannot afford the shipment of the goods then worker could add another container to solve the problem.





# Reference Links

About container & container orchestration:
https://blog.newrelic.com/engineering/container-orchestration-explained/
