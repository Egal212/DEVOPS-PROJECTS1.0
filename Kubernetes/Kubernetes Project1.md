This project will be using the minikube to create a Mongo-express web app and a Mongo-DB database.
There will be two deployments or pods, two services, two config maps, and one secret will be created for this project.

COMPONENTS OF THE PROJECTS.
I will be creating;
- Using a CONFIG.MAP to create a MongoDB deployment and an internal service which means no external requests are allowed to the pod, only components from the cluster can communicate.
- Use a config. map to create a mongo-express web application and an external service needed to communicate externally through the browser, and will also need the MongoDB URL to connect to the database via the credentials (username and password) of the database for authentication which will be stored in the secret but referenced via environmental variables in the config. map.
- Create a secret that contains the database credentials that are used for authentication in the mongo-express and database. This helps to connect the database to the web application.

Confirm all the components that are currently in the kubectl using this command :

``
kubectl get all
``
# 1.Create a secret using the secret-config map.
In Kubernetes, a Secret is an object that allows you to store and manage sensitive information, such as passwords, API keys, tokens, or any confidential data that your application needs. Secrets are designed to keep this sensitive data secure within a Kubernetes cluster.
The crypt text was created by running this command:

``
echo -n 'username' | base64
echo -n 'password' | base64
``

![Screenshot 2023-09-17 at 20 21 22](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/d9c11ddb-8460-402b-a12c-462fd7cf5f44) 

After creating the encryption I input the encrypted text into the secret config. map and created the secret.

Copy and paste this file to create a secret for the MongoDB deployment you will be creating and name it mongodb-secret.yaml.
```
apiVersion: v1
kind: Secret
metadata:
    name: mongodb-secret
type: Opaque
data:
    mongo-root-username: dXNlcm5hbWU=
    mongo-root-password: cGFzc3dvcmQ=
``
Use this command to create the secret:

``
kubectl apply -f mongodb-secret.yaml
kubectl delete -f mongodb-secret.yaml
```

![Screenshot 2023-09-17 at 20 14 26](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/991453ec-1904-4483-bd4a-57acf39528b4)

![Screenshot 2023-09-17 at 20 18 45](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/8d912f2f-d540-49f7-ba87-308beae619a8)



# 2. Create a MongoDB Database deployment using Config.map
I created a config. map in a text editor that will be checked into a repository.
Note: Do not write the username and password of the database or sensitive credentials in the config. map.

Copy and paste this example config.map for MongoDB into the file which I will be calling Mongo.yaml. This file will contain the deployment name, labels, selectors, specification, ports, and database root username and password which was stored in the secret config.map that was created earlier.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-deployment
  labels:
    app: mongodb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      labels:
        app: mongodb
    spec:
      containers:
      - name: mongodb
        image: mongo
        ports:
        - containerPort: 27017
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-username
        - name: MONGO_INITDB_ROOT_PASSWORD
          valueFrom: 
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-password
```


This file will be used to create the Mongodb database for deployment.
Navigate to the terminal into the file and create the deployment using the command:

``
kubectl apply -f <mongo.yaml>
``

![Screenshot 2023-09-17 at 19 47 34](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/6511e6f1-c547-4318-9936-538d567248f5)

# 3.  Create the internal service.

Create the internal service by either creating a separate config.map for the service or adding the service configuration map to the deployment config.map using ---. The file will look like this:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-deployment
  labels:
    app: mongodb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      labels:
        app: mongodb
    spec:
      containers:
      - name: mongodb
        image: mongo
        ports:
        - containerPort: 27017
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-username
        - name: MONGO_INITDB_ROOT_PASSWORD
          valueFrom: 
            secretKeyRef:
              name: mongodb-secret
              key: mongo-root-password
---
apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
spec:
  selector:
    app: mongodb
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
```
After configuring the service to the deployment file I then created the service without changing the deployment file using this command:

``
kubectl apply -f <mongo.yaml>
``

![Screenshot 2023-09-17 at 20 26 48](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/9da3872e-47fc-4606-8132-e61adce00fe0)


4. Verify the deployment and service using this command:
   
``
kubectl get all
``

![Screenshot 2023-09-17 at 20 29 09](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/afce236a-d38a-4228-9ba1-a16944c72e7f)

Use this command to confirm that the service is running on the right pod.

``
kubectl describe service mongodb-service
kubectl get pod -o wide
``

![Screenshot 2023-09-17 at 20 32 41](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/f89189ca-32cc-46ac-a287-7da82c433e9c)

You will notice that the IP address for the MongoDB service is the same as the mongodb-deployment service.



