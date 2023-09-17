# MINIKUBE

MINIKUBE: is a test or local setup where both the master and worker node processes run on one machine with docker container run-time pre-installed that runs on your laptop through a virtual box or hypervisor.

MINIKUBE FEATURES.
* creates a virtual box on your laptop.
* creates the nodes that run in that virtual box.

# KUBECTL
KUBECTL: is a CLI tool for kubernetes cluster used to interact with kubernetes.

CREATING A DEPLOYMENT USING KUBECTL
In kubernetes pod is the smalest unit, therefore you cannot creat a pod but rather you create a deployment.

The command syntax for creating a deployment is : 
``
kubectl create deployment <NAME> --image=image
``
Pods are created from images.
EXAMPLE: 
Creating a pod from nginx 
``
Kubectl create deployment nginx-depl --image=nginx
``
By creating a deployment you create the blueprint for creating pods , and the most basic configuration for deployment.
You also create the replicaset which isthe kubernetes tool used in mnageing the replias of the pod. This is automatially managed ny kubernetes.

Common Kubectl commnds 
``
kubectl logs
kubectl exec -it
kubectl edit deployment <DEPLOYMENT NAME>
``
