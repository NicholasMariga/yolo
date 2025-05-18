In this README.md is on both MINIKUBE and GKE as Orchestrators 


################ MINIKUBE ################

Deploying your full-stack application (client (Frontend) + Backend + MongoDB) on Minikube, 
including 
    - Docker image building, 
    - Kubernetes deployment, 
    - service exposure, 
    - key project explanations.


# Full-Stack Kubernetes App on Minikube (Frontend + Backend + MongoDB)

This project demonstrates a full-stack web application composed of a React frontend, a Node.js backend, and MongoDB for storage. The app is containerized with Docker and deployed locally using Minikube and Kubernetes.



## Tech Stack

- Client (Frontend): Node.js
- Backend: Node.js + Express
- Database: MongoDB
- Orchestration: Kubernetes (Minikube)
- Storage: PersistentVolume for MongoDB
- Containerization: Docker



## Project Structure

.
├── backend/
│   └── Dockerfile
├── client/
│   └── Dockerfile
├── manifests/
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── client-deployment.yaml
│   ├── client-service.yaml
│   ├── mongo-statefulset.yaml
│   └── mongo-service.yaml
├── explanation.md
└── README.md





##  Prerequisites

- Docker
- Minikube installed
- kubectl installed



##  Steps to Run Locally with Minikube

### 1. Start Minikube
On terminal

    minikube start



### 2Build Docker Images

Backend

cd backend
docker build -t marigah/backend-service:v2.0.0


Frontend

cd ../client
docker build -t marigah/client-service:v2.0.0


### 3 Apply Kubernetes Manifests

bash
cd ../k8s

kubectl apply -f mongo-service.yaml
kubectl apply -f mongo-statefulset.yaml

kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-service.yaml

kubectl apply -f client-deployment.yaml
kubectl apply -f client-service.yaml


### 4. Expose client(Frontend) Service


minikube service client-service


This will open the app in your default browser using Minikube’s IP and NodePort.

