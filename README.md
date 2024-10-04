Simple WebApp Flask - CI/CD with Local Kubernetes Cluster in Docker Desktop

Overview

This project is a simple Flask web application that provides a basic API functionality. The application is containerized using Docker, and the deployment is automated using Kubernetes in a local environment via Docker Desktop, with GitHub Actions managing the CI/CD pipeline.

Project Summary

API Functionality

The API serves as a basic web application using Flask. It listens on port 5000 and provides simple responses to HTTP requests, making it ideal for learning how to containerize and deploy web applications. The API could be expanded to include more complex endpoints and functionality, but for now, it is a basic demonstration of Flask capabilities.

Containerization

The API is containerized using Docker. The Dockerfile defines the environment, specifying the base image (python:3.x), installing the required dependencies, and copying the application code into the container. The Docker container can be built and run locally using the following commands:

docker build -t simple-webapp-flask:latest .
docker run -p 5000:5000 simple-webapp-flask

This Docker container ensures that the application and all its dependencies are bundled together, making it easy to deploy in different environments.

CI/CD Process

The CI/CD pipeline is implemented using GitHub Actions. The workflow file located at .github/workflows/ci-cd.yaml is used to automate the following tasks:

Build: The Docker image of the application is built whenever changes are pushed to the main branch.

Push: The Docker image is pushed to Docker Hub for storage and later retrieval.

Deploy: After the image is pushed, it is deployed to a local Kubernetes cluster using kubectl commands. The CI/CD pipeline is triggered by any code changes, allowing for continuous integration and deployment of new features.

Kubernetes Deployment

The application is deployed to a local Kubernetes cluster using Docker Desktop's Kubernetes feature. The deployment process involves:

Creating Kubernetes Manifests: The deployment.yaml and service.yaml files are used to define the deployment of the Flask application and expose it as a service within the cluster.

Applying Manifests: The manifests are applied using kubectl commands, which create pods, services, and other necessary Kubernetes resources to run the application.

Accessing the Application: The service is accessed using kubectl port-forward to expose the service endpoint to localhost, making it accessible via http://localhost:5000.

Security Measures

Docker Image Security: The Docker image is kept minimal, based on a secure Python base image, reducing the attack surface.

Kubernetes Role-Based Access Control (RBAC): Although not fully implemented in this version, RBAC can be used to limit permissions and secure access to the cluster.

Secrets Management: Sensitive information, such as Docker Hub credentials and kubeconfig data, is managed using GitHub Secrets, ensuring they are not hard-coded into the source code.

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