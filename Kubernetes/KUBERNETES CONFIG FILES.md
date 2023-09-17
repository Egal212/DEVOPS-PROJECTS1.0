Kubernetes config file typically refers to a Kubernetes configuration file or a kubeconfig file. This file is used to configure various aspects of the Kubernetes command-line tool (kubectl) and set the context for interacting with Kubernetes clusters. It contains information about clusters, users, and contexts.

CREATING A BASIC NGINX DEPLOYMENT USING THE CONFIG FILE.
``
touch nginx-deployment.yaml
vim nginx-deployment.yaml
``
Copy and paste this code into the file.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.16
        ports:
        - containerPort: 8080

```

Use the following command to create and delete the application file.

``
kubectl apply -f <deployment-name.yaml>
kubectl delete -f <deployment-name.yaml>
``
This command will create and delete the deployments which will contain the pod and two replicaset and will pull an nginx image with version 1.16 and set the container port 8080.







