# mongo-express-with-mongodb-on-k8s
Deploying MongoDB and Mongo Express on a Minikube kubernetes cluster.
<div align="center">
<img src="https://user-images.githubusercontent.com/47721226/222544094-24782066-4c50-41f7-bc8a-2f94cab0b0e6.png">
</div>

## Prerequisite
Minikube cluster running \
[minikube installation](https://minikube.sigs.k8s.io/docs/start/)

## Steps
### 1. Create Secret for MongoDB Credentials
* Encrypt MongoDB credentials
* Create MongoDB secret configuration file `mongo-secret.yaml` with these credentials 
* Create MongoDB secret `kubectl apply -f mongo-secret.yaml`
* Check the created Secret `kubectl get secret`\
![image](https://user-images.githubusercontent.com/47721226/222548184-5a74846d-ac0f-4ed9-b5d1-749da67a3260.png)

### 2. Create MongoDB Deployment
* Create MongoDB Deployment configuration file `mongo.yaml` using [mongo image](https://hub.docker.com/_/mongo)
* Create MongoDB Deployment `kubectl apply -f mongo.yaml`
* Check the created deployment `kubectl get all`\
![image](https://user-images.githubusercontent.com/47721226/222549890-2d4683d8-c7f6-43a4-bdbb-6ce1924f8723.png)

### 3. Create MongoDB Internal Service
* Create internal service (ClusterIP) configuration file `mongo-service.yaml` using `port:27017` and `targetPort:27017`
* Create MongoDB serivce `kubectl apply -f mongo-service.yaml`
* Check if the service is created on the right pod `kubectl describe svc mongodb-service` and `kubectl get pod -o wide`\
![image](https://user-images.githubusercontent.com/47721226/222553545-d8b4641c-481f-4d23-8909-2d512661c0c7.png)

### 4. Create ConfigMap for DB Server URL
* Creat MongoDB ConfigMap configuration file `mongo-configmap.yaml` with DB-URL
* Create MongoDB ConfigMap `kubectl apply -f mongo-configmap.yaml`

