# simple-webapp-flask
Assessment 2 for DevSecOps Cybergirls



Simple WebApp Flask - CI/CD with Local Kubernetes Cluster in Docker Desktop

Overview

This project is a simple Flask web application, containerized with Docker, and deployed to a Kubernetes cluster using GitHub Actions for CI/CD. The Kubernetes cluster is set up locally using Docker Desktop, which helps in simulating a production-like environment without the need for cloud services. This project demonstrates end-to-end automation for deploying a Python-based web application, including build, containerization, and deployment.

Prerequisites

Docker Desktop installed with Kubernetes enabled

kubectl installed for interacting with Kubernetes clusters

A GitHub account to manage the repository and secrets for the CI/CD pipeline

Project Structure

app.py: The main Python script containing the Flask application code.

Dockerfile: Defines the environment and instructions for containerizing the application.

deployment.yaml & service.yaml: Kubernetes manifests for deploying the Flask app and exposing it as a service.

.github/workflows/ci-cd.yaml: GitHub Actions workflow script for automating the build, push, and deployment process.

Getting Started

Step 1: Clone the Repository

Clone this repository to your local machine:

git clone https://github.com/TomiAdeniji/simple-webapp-flask.git
cd simple-webapp-flask

Step 2: Docker Setup

To build and run the Docker container locally:

docker build -t simple-webapp-flask:latest .
docker run -p 5000:5000 simple-webapp-flask

Visit http://localhost:5000 in your browser to see the application running locally.

Step 3: Set Up Local Kubernetes Cluster with Docker Desktop

Enable Kubernetes in Docker Desktop:

Open Docker Desktop settings.

Go to the Kubernetes tab and check Enable Kubernetes.

Wait for Kubernetes to be enabled and running.

Verify Kubernetes Setup:

kubectl config get-contexts

Ensure that the Docker Desktop Kubernetes context is set as the current context.

Step 4: Deploy to Local Kubernetes Cluster

Build Docker Image for Local Kubernetes:
Ensure the image is available within the local cluster:

docker build -t simple-webapp-flask:latest .

Apply Kubernetes Manifests:

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

Access the Application:
Use kubectl port-forward to access the service:

kubectl port-forward service/flask-app-service 5000:5000

Visit http://localhost:5000 to see the application running.

Step 5: GitHub Actions Setup

Add GitHub Secrets:

DOCKER_HUB_USERNAME and DOCKER_HUB_ACCESS_TOKEN: Docker Hub credentials to allow the workflow to push images.

CI/CD Workflow:

The .github/workflows/ci-cd.yaml file handles building the Docker image, pushing it to Docker Hub, and deploying it to the local Kubernetes cluster (if applicable).

Step 6: Trigger the CI/CD Pipeline

Push any changes to the main branch to trigger the CI/CD pipeline.
The GitHub Actions workflow will:

Build and push the Docker image to Docker Hub.

Deploy the updated image to the local Kubernetes cluster using kubectl commands.

Project Workflow

Code Changes: Make any changes to the Python code in app.py.

Commit and Push: Commit changes and push them to the main branch.

CI/CD Pipeline: GitHub Actions automatically runs the workflow to build, push, and deploy the updated container.

Verify Deployment: Access the application locally to verify the updated deployment.

Key Technologies

Python & Flask: The core web application.

Docker: For containerizing the application.

Docker Desktop Kubernetes: For hosting the local Kubernetes cluster.

GitHub Actions: For CI/CD automation.

Troubleshooting

Kubernetes Access Issue: Ensure your kubeconfig is properly configured for Docker Desktop Kubernetes.

Container Build Failure: Verify the Dockerfile syntax and ensure Docker is installed and running locally.

Pipeline Failures: Check the logs in the GitHub Actions tab for detailed error messages.

Future Enhancements

Monitoring and Alerts: Integrate Prometheus and Grafana for monitoring the Kubernetes cluster.

Scalability: Experiment with autoscaling using Horizontal Pod Autoscaler (HPA).

Security: Implement role-based access control (RBAC) and secure environment variables.