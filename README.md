# Kubernetes Web App Deployment

This project demonstrates a complete DevOps workflow: containerizing a static web application, deploying it to a local Kubernetes cluster (Minikube), and managing the deployment using **Helm**.

## 🚀 Features
- **Dockerization**: Custom Nginx image containing a unique "Hello, Kubernetes!" landing page.
- **Helm Orchestration**: Reusable templates for Deployment and Service objects.
- **Resource Management**: Configured CPU and Memory requests/limits (100m/64Mi requests, 200m/128Mi limits) to ensure cluster stability.
- **Health Checks**: Implemented Liveness Probes to monitor container health on port 80.
- **Scalability**: Configured for 2 replicas by default in `values.yaml`.

---

## 🛠️ Prerequisites
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Helm](https://helm.sh/docs/intro/install/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

---

## 🏃 Getting Started

### 1. Build the Docker Image
created a custom `index.html` and a `Dockerfile` to serve it using Nginx.

```bash
docker build -t myapp:latest .