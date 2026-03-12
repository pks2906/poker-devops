# Poker Microservices Platform – DevOps CI/CD Deployment

This repository contains a **containerized microservices poker platform** along with a complete **DevOps CI/CD pipeline and Kubernetes deployment setup**.

The original poker application was developed by another contributor and this repository is a **fork** of that project.  
My contributions focus on **DevOps infrastructure, containerization, CI/CD automation, and Kubernetes deployment**.

---

# Architecture

```text
Developer Push
     │
     ▼
   GitHub Repository
     │
     ▼
   Jenkins CI/CD Pipeline
     │
     ├── Build Docker Images
     │
     ├── Push Images → DockerHub
     │
     ▼
Kubernetes Deployment (Minikube)
     │
     ▼
NGINX Ingress Controller
     │
     ├── poker.local  → User Frontend
     │
     ├── admin.poker.local → Admin Frontend
     │
     ▼
Backend API  ←→  WebSocket Server
     │
     ▼
PostgreSQL (StatefulSet + Persistent Volume)
```

This architecture enables **automated deployment of a multi-service platform using CI/CD pipelines and Kubernetes orchestration.**

---

# Microservices

The platform consists of the following services:

- Backend API
- WebSocket server
- User frontend
- Admin frontend
- PostgreSQL database

All services are **containerized using Docker** and deployed on **Kubernetes**.

---

# DevOps Features Implemented

### CI/CD Pipeline (Jenkins)

A Jenkins pipeline was implemented to automate the entire workflow.

Pipeline stages:

1. Clone repository from GitHub
2. Build Docker images for all services
3. Push images to DockerHub
4. Deploy services to Kubernetes using `kubectl`

This creates a **fully automated build → push → deploy pipeline**.

---

### Containerization (Docker)

All application services were containerized using **Docker**.

Services containerized:

- backend
- websocket
- user-frontend
- admin-frontend

Docker Compose is used to run the entire system locally for development.

---

### Kubernetes Deployment

The application is deployed on **Kubernetes (Minikube)** using:

- Deployments
- Services
- StatefulSets
- Ingress
- Persistent Volumes
- Persistent Volume Claims

This provides **scalable orchestration and service discovery**.

---

### Persistent Database Storage

PostgreSQL is deployed using a **StatefulSet** with persistent storage.

Components used:

- Persistent Volume (PV)
- Persistent Volume Claim (PVC)

This ensures:

- durable storage
- stable pod identity
- safe database restarts

---

### Ingress Routing

An **NGINX Ingress Controller** routes external traffic to services.

Example routing:

| Host | Service |
|-----|------|
| poker.local | User Frontend |
| admin.poker.local | Admin Frontend |

This creates a **single entry point for external traffic into the cluster**.

---

# Tech Stack

| Category | Technology |
|--------|-------------|
| CI/CD | Jenkins |
| Containers | Docker |
| Container Registry | DockerHub |
| Orchestration | Kubernetes (Minikube) |
| Database | PostgreSQL |
| Networking | NGINX Ingress |
| Runtime | Bun / Node.js |

---

# Running the Project Locally

## 1. Clone the repository

```bash
git clone https://github.com/pks2906/poker-devops.git
cd poker-devops
```

---

## 2. Run services with Docker Compose

```bash
docker compose up -d
```

This starts:

- backend
- websocket
- user frontend
- admin frontend
- postgres

---

## 3. Start Kubernetes cluster

```bash
minikube start
```

Enable ingress:

```bash
minikube addons enable ingress
```

---

## 4. Deploy to Kubernetes

```bash
kubectl apply -f k8s/
```

Verify deployment:

```bash
kubectl get pods -n poker
```

---

## 5. Configure local hosts

Edit the hosts file:

```bash
sudo nano /etc/hosts
```

Add:

```
$(minikube ip) poker.local
$(minikube ip) admin.poker.local
```

---

## 6. Access the application

Open in browser:

```
http://poker.local
http://admin.poker.local
```

---

# CI/CD Pipeline

The Jenkins pipeline automatically performs:

1. Checkout repository
2. Build Docker images
3. Push images to DockerHub
4. Deploy application to Kubernetes

Pipeline configuration is stored in:

```
Jenkinsfile
```

---

# Docker Images

Images built and pushed to DockerHub:

```
pks2906/poker-backend
pks2906/poker-websocket
pks2906/poker-user-frontend
pks2906/poker-admin-frontend
```

---

# My DevOps Contributions

In this forked repository, I implemented:

- Docker containerization for all services
- Docker Compose development environment
- Kubernetes manifests for deployments and services
- PostgreSQL StatefulSet with persistent storage
- NGINX ingress configuration
- Jenkins CI/CD pipeline
- Automated Docker image builds and pushes
- Kubernetes automated deployment pipeline

---

# Learning Outcomes

Through this project I gained hands-on experience with:

- CI/CD pipeline design
- containerized microservices architecture
- Kubernetes orchestration
- infrastructure automation
- DevOps troubleshooting and debugging

---

# Future Improvements

Planned improvements include:

- Helm charts for Kubernetes deployments
- GitHub webhook integration with Jenkins
- Prometheus + Grafana monitoring
- Deployment to cloud Kubernetes platforms (AWS EKS)

---

# License

This repository is a fork of the original project and is used for **educational and DevOps learning purposes**.
