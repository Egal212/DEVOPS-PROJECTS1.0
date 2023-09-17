# KUBERNETES 
Kubernetes is an open-source container orchestration tool that helps to manage containerized applications in different development environments.

# KUBERNETES FEATURES
* High availability and no downtime.
* Scalability or high performance.
* Disaster recovery,  backup or restore.

# KUBERNETES COMPONENT.
* Nodes: is a simple server which can be physical or a virtual machine.

* Pods: are the smallest unit of Kubernetes service. Pods create the running environment or a layer on top of the container. It's usually one pod per application. Since Kubernetes offers a virtual network, each pod has an IP address. Pods communicate with each other via that IP address.
Pods components in Kubernetes are temporary which means they die quickly. If one pod dies another gets created easily which means a new IP address will be created upon a re-creation of the pod.

* Service and Ingress: a static or permanent IP address that can be attached to each pod. The lifecycle of the pods is not connected which means if the pod dies the service persists.

* External service: is a service that opens the communication from external services. In order for your app to be accessible through a browser, you will need to create an external service.

* Internal service: is a type of service that you specify when creating pods. It helps you to communicate within the pod.

* Ingress: is what helps you to communicate to Kubernetes via a domain name.

* Config.Map; is your external configuration file for your application. It contains configuration data like database URLs or some services used in Kubernetes that are connected to the pod, therefore the pod gets its data from the config. map. Whenever you would like to update or change the details of an image you can do so in the config map without building a new image.
Note: Do not put credentials in your config. map.

* Secret: is like an external config. map but used to store secret data and credentials, not in place text but in base 64 encoded. You can connect data from secret to your config. map via environmental variables.



