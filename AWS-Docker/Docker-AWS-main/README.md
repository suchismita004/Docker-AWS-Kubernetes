
# 🕷️ Python Scraper with Docker, Kubernetes, AWS EKS & Lambda Integration

This project contains a Python-based web scraper containerized using Docker, orchestrated via Kubernetes (Minikube and AWS EKS), and also deployed as a serverless function using AWS Lambda.

---

## 📁 Project Structure

```bash
.
├── scrapper.py               # Main web scraping script
├── Dockerfile                # Docker configuration
├── deployment.yaml           # Kubernetes deployment manifest
├── service.yaml              # Kubernetes service manifest
├── lambda_function.py        # Lambda-compatible version of scraper
├── requirements.txt          # Python dependencies
```

---
## ✅ Requirements

- Docker
- Minikube
- kubectl
- AWS CLI
- eksctl
- Python 3.9+

---
## 🐳 Docker Setup

### ✅ Build Docker Image

```bash
docker build -t python-scraper .
```

### ▶️ Run the Container

```bash
docker run -d --name scraper-container python-scraper
```

### 🔎 Check Logs

```bash
docker logs scraper-container
```

---

## ☸️ Kubernetes with Minikube

### 🚀 Start Minikube

```bash
minikube start
```

### 🛠️ Deploy to Minikube

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### 📡 Access the Service

```bash
minikube service scraper-service
```

### 📋 Check Pods

```bash
kubectl get pods
```

### 🔍 View Logs

```bash
kubectl logs <pod-name>
```

---

## ☁️ AWS EKS Setup

### 1️⃣ Create an EKS Cluster (CLI Example)

```bash
eksctl create cluster --name scraper-cluster --region us-west-2 --nodes 2
```

### 2️⃣ Update `kubectl` Context

```bash
aws eks --region us-east-1 update-kubeconfig --name scraper-cluster
```

### 3️⃣ Deploy on EKS

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---


## 🦥 AWS Lambda Deployment

### ✅ Create Lambda Package

```bash
pip install -r requirements.txt -t lambda-package/
cp lambda_function.py lambda-package/
cd lambda-package
zip -r9 ../scraper-lambda.zip .
```

### 🚀 Deploy via AWS CLI

```bash
aws lambda create-function \
  --function-name scraperLambda \
  --runtime python3.9 \
  --role arn:aws:iam::<your-account-id>:role/<lambda-execution-role> \
  --handler lambda_function.lambda_handler \
  --zip-file fileb://scraper-lambda.zip
```
