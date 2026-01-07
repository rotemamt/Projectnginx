Kubernetes Web App Deployment
This project demonstrates a complete DevOps workflow: containerizing a static web application, deploying it to a local Kubernetes cluster (Minikube), and managing the deployment using Helm.
🚀 Features

Dockerization: Custom Nginx image containing a unique "Hello, Kubernetes!" landing page.
Helm Orchestration: Reusable templates for Deployment and Service objects.
Resource Management: Configured CPU and Memory requests/limits (100m/64Mi requests, 200m/128Mi limits) to ensure cluster stability.
Health Checks: Implemented Liveness Probes to monitor container health on port 80.
Scalability: Configured for 2 replicas by default in values.yaml.


🛠️ Prerequisites

Docker Desktop
Minikube
kubectl
Helm


🏃 Getting Started
1. Build the Docker Image
I created a custom index.html and a Dockerfile to serve it using Nginx.
bashdocker build -t myapp:latest .
2. Kubernetes Deployment (Static)
The application can be deployed using standard Kubernetes manifests. This deployment is configured with 2 replicas for high availability.
Prepare Minikube:
bashminikube start
minikube image load myapp:latest
Deploy using Static YAMLs:
bashkubectl apply -f deployment.yml
kubectl apply -f service.yml
3. Access & Verification
To access the application from the local machine, use port-forwarding to map the cluster's internal port to 8080.
Command:
bashkubectl port-forward svc/myapp-service 8080:80
URL: http://localhost:8080
4. Bonus: Helm Chart Deployment
The entire application is also packaged as a Helm chart in the /myapp directory for configurable deployments.
Install the Chart:
bashhelm install myapp ./myapp
Why Helm? It centralizes configuration (replicas, image tags, and resource limits) within a single values.yaml file, making the deployment more manageable and scalable.

📂 Project Structure

index.html: The static web page.
Dockerfile: Instructions for building the custom Nginx image.
deployment.yml / service.yml: Static Kubernetes manifests.
myapp/: The Helm Chart directory.

values.yaml: Main configuration file for the chart.
templates/: YAML templates for the deployment and service.




🧹 Cleanup
To remove the resources from your cluster:
bash# If using Helm
helm uninstall myapp

# If using static manifests
kubectl delete -f deployment.yml -f service.yml
