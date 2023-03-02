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
* Create MongoDB deployment configuration file `mongo.yaml` using [mongo image](https://hub.docker.com/_/mongo)
* Create MongoDB deployment `kubectl apply -f mongo.yaml`

### 3. Create MongoDB Internal Service
* Create internal service (ClusterIP) configuration file `mongo-service.yaml` using `port:27017` and `targetPort:27017`
* Create MongoDB serivce `kubectl apply -f mongo-service.yaml`
* Check if the service is created on the right pod using `kubectl describe svc mongodb-service` and `kubectl get pod -o wide`\
![image](https://user-images.githubusercontent.com/47721226/222553545-d8b4641c-481f-4d23-8909-2d512661c0c7.png)

### 4. Create ConfigMap for DB Server URL
* Creat MongoDB configMap configuration file `mongo-configmap.yaml` with DB-URL
* Create MongoDB configMap `kubectl apply -f mongo-configmap.yaml`

### 5. Create MongoExpress Deployment
* Create MongoExpress configuration file `mongo-express.yaml` using [mongo-express image](https://hub.docker.com/_/mongo-express)
* Create MongoExpress deployment `kubectl apply -f mongo-express.yaml`

### 6. Create Mongo Express External Service
* Create external service (LoadBalancer) configuration file `mongo-express-service.yaml` using `port: 8081` , `targetPort: 8081` and `nodePort: 30000`
* Create Mongo Express service `kubectl apply -f mongo-express-service.yaml`
* Check if the service is created on the right pod using `kubectl describe svc mongo-express-service` and `kubectl get pod -o wide`\
![image](https://user-images.githubusercontent.com/47721226/222558080-f4b3ff05-c213-4d95-8759-663ab81f99c9.png)

### 7. Validation
* Assign a public IP for the external service `minikube service mongo-express-service`\
![image](https://user-images.githubusercontent.com/47721226/222560452-1979e71d-a02b-4cfe-aac0-7a80b156e562.png)
* Use the assigned IP to access the service\
![image](https://user-images.githubusercontent.com/47721226/222560605-1b0481e7-0ed7-44a2-a8af-dcd3ef85c293.png)

