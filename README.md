# Devops_Assignment_Ilham

🚀 Flask-MongoDB Deployment on Minikube
This README provides step-by-step instructions to deploy a Flask application connected to MongoDB on a Minikube Kubernetes cluster.

---

## 📝 Prerequisites

Before you begin, ensure that you have the following installed on your machine:

- **Minikube** 🚀
- **Kubectl** 🛠️
- **Docker** 🐳
- **Python 3.8+** 🐍

---

## 📂 Structure

```
flask-mongodb-app/
│
├── app.py
├── requirements.txt
├── Dockerfile
│
├── k8s/
│   ├── flask_deployment.yaml
│   ├── flask_service.yaml
│   ├── mongodb_stateful.yaml
│   ├── mongodb_service.yaml
│   ├── flask_hpa.yaml
│
├── .env
└── README.md
```

---

## ⚙️ Step 1: Set Up Minikube

Start Minikube:

```bash
minikube start
```

---

## 🛠️ Step 2: Build and Push Docker Image

Build the Docker Image:

```bash
docker build -t docker_hub-username/flask-mongodb-app .
```

(Optional) Push the Docker Image to Docker Hub:

```bash
docker push docker_hub-username/flask-mongodb-app
```

---

## 📦 Step 3: Deploy MongoDB on Kubernetes

Create Kubernetes Secret for MongoDB Authentication:

```bash
kubectl create secret generic mongodb-secret \
  --from-literal=MONGO_INITDB_ROOT_USERNAME=myUser \
  --from-literal=MONGO_INITDB_ROOT_PASSWORD=myPassword \
  --from-literal=MONGO_DBNAME=flask_db
```

Deploy MongoDB StatefulSet:

```bash
kubectl apply -f k8s/mongodb_stateful.yaml
```

Deploy MongoDB Service:

```bash
kubectl apply -f k8s/mongodb_service.yaml
```

---

## 🚀 Step 4: Deploy Flask Application on Kubernetes

Deploy Flask Application:

```bash
kubectl apply -f k8s/flask_deployment.yaml
```

Deploy Flask Service:

```bash
kubectl apply -f k8s/flask_service.yaml
```

---

## 📊 Step 5: Set Up Horizontal Pod Autoscaler (HPA)

Deploy HPA for Flask Application:

```bash
kubectl apply -f k8s/flask_hpa.yaml
```

---

## 🔍 Step 6: Access the Application

Get Minikube IP Address:

```bash
minikube ip
```

This command will return the ip address where the Flask application is accessible.

Test the Application:

### Access Welcome Page:

```bash
curl http://<Minikube_IP>:<NodePort>/
```

### POST Data to MongoDB:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' http://<Minikube_IP>:<NodePort>/data
```

### GET Data from MongoDB:

```bash
curl http://<Minikube_IP>:<NodePort>/data
```

---

## 🎉 Congratulations!

Your Flask application connected to MongoDB is now deployed on Minikube! 🎊

---