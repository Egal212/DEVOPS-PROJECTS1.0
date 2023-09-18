It is very important to create the components in a certain order.
For example, before you can apply a config. map to a web app you have to create the config. map.

# CREATING A CONFIG.MAP.YAML FOR THE DATABASE.
Copy and paste this code to create the config.map and name it mongo-configmap.yaml
``
apiVersion: v1
kind: ConfigMap
metadata:
  name: mongodb-configmap
data:
  database_url: mongodb-service
  ``
  Create the config map by running:
  ``
  kubectl apply -f mongo-configmap.yaml
  ``
![Screenshot 2023-09-17 at 20 46 28](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/0fef7b11-8dd4-42b2-8c16-391f5286caf7)

Create the Mongo-express web application deployment by 
Copy and Write the mongo-express.yaml file 
``
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo-express
  labels:
    app: mongo-express
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo-express
  template:
    metadata:
      labels:
        app: mongo-express
    spec:
      containers:
      - name: mongo-express
        image: mongo-express
        ports:
        - containerPort: 8081
        env:
        - name: ME_CONFIG_MONGODB_ADMINUSERNAME
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-username
        - name: ME_CONFIG_MONGODB_ADMINPASSWORD
          valueFrom: 
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-password
        - name: ME_CONFIG_MONGODB_SERVER
          valueFrom: 
            configMapKeyRef:
              name: mongodb-configmap
              key: database_url
              ``
This file contains the labels, exposes the ports and 
the container ports, the name and image used, and the environmental variables which include the mongodb database address/Internal service,  mongodb admin username and admin password,mongodb configmap  the secret key ref with the name of the secret and credentials, and the config.map for the database URL.

create the deployment with the command 
``
kubectl apply -f mongo-express.yaml
kubectl get pod
``
![Screenshot 2023-09-18 at 12 52 38](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/dcf59328-4220-4452-ae6e-abb913687c9f)

![Screenshot 2023-09-18 at 13 18 58](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/b0d9533a-2e77-49f6-8c66-ece5028d1eed)

* Next you want to view the logs to confirm that the mongo-express webapp has connected to the mongodb database using
 ``
kubectl logs <deployment-name>
``
![Screenshot 2023-09-18 at 14 48 00](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/fb460d84-2be6-4b7e-ab0f-c292c68e9070)



Next you want to create an external service for that web appl deployment that can connect to the webapp through the browser.
Copy and paste this config.map tht contains the service you will be creating:

``---
apiVersion: v1
kind: Service
metadata:
  name: mongo-express-service
spec:
  selector:
    app: mongo-express
  type: LoadBalancer  
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 8081
      nodePort: 30000
``

The service details the kind , the service name nd the specification which details the selector with the app anme nd the type which is loadbalancer and the port used and the port number. Another feature it detailed is the nodeport. Nodeport is the port where the external service ip address will be open. It has a range of 30000- 32767.

The type loadbalancer is used to create an external service because when you create the external service you get both the internal cluster ip address and the external ip address.

create the service by running the same mongo-express configmao file becuase i saved both the service nd deployment on the same file and verify the service by running:
..
``
kubectl apply -f mongo-express.yaml
kubectl get service
``
![Screenshot 2023-09-18 at 14 49 00](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/a50f9f1a-22e3-4369-92e3-2faeaeac08ee)

To get for the external Ip address for the external service that will be used to communiate to the web app through the browser.
``
minikube service mongo-express-service

``![Screenshot 2023-09-18 at 14 52 41](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/9ea1a503-fcbf-4404-b283-c7246c1453b7)

You click the https link and you have a web view of this image.

![Screenshot 2023-09-17 at 00 33 58](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/4207213f-2ddd-41be-a8cf-a1dceeda1c93)

That is how you createa mongodb database and mongo-express webapp in a minikube.

# CLEANUP
DELETE ALL RESOURCES USING THE FOLLOWING COMMANDS:
``
kubectl delete -f <mongo-db deployment-filename.yaml>
kubectl delete -f <mongo-db config-mapfile-name.yaml>
kubectl delete -f <mongo-express deploymentfile-name.yaml>
kubectl delete -f <secret configmapfile-name.yaml>
``

![Screenshot 2023-09-18 at 14 58 15](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/a8ca7de0-f76d-4ab8-a96d-e10da7788cf6)








