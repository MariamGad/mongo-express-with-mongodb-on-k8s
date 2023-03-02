# mongo-express-with-mongodb-on-k8s
Deploying MongoDB and Mongo Express on a Minikube kubernetes cluster.
<div align="center">
<img src="https://user-images.githubusercontent.com/47721226/222544094-24782066-4c50-41f7-bc8a-2f94cab0b0e6.png">
</div>

## Prerequisite
Minikube cluster running \
[minikube installation](https://minikube.sigs.k8s.io/docs/start/)

## Steps
### 1. Create a Secret for MongoDB Credentials
* Encrypt mongoDB credentials
* Create mongoDB secret configuration file `mongo-secret.yaml`
* Create mongoDB secret `kubectl apply -f mongo-secret.yaml`
* Check the created Secret `kubectl get secret`\
![image](https://user-images.githubusercontent.com/47721226/222548184-5a74846d-ac0f-4ed9-b5d1-749da67a3260.png)

### 2. Create MongoDB Deployment
* Create mongoDB Deployment configuration file `mongo.yaml`
* Create MongoDB Deployment `kubectl apply -f mongo.yaml`
* Check the created deployment `kubectl get all`\
![image](https://user-images.githubusercontent.com/47721226/222549890-2d4683d8-c7f6-43a4-bdbb-6ce1924f8723.png)
