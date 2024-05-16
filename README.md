# Operation

## Overview

This repository is part of the REMLA24-Team3 project and serves as the central hub for running and operating the URL Phishing detection application. 
It contains Docker Compose configurations to facilitate easy deployment and operation of the application.

### Related Repositories

- [Model Training](https://github.com/remla24-team3/model-training)
- [Model Service](https://github.com/remla24-team3/model-service)
- [Library for Machine Learning (lib-ml)](https://github.com/remla24-team3/lib-ml)
- [Library for Versioning (lib-version)](https://github.com/remla24-team3/lib-version)
- [Application Frontend and Service (app)](https://github.com/remla24-team3/app)

## Getting Started

### Prerequisites

- Docker and Docker Compose installed on your machine.
- Access to the internet to pull container images and dependencies.

### Running the Application

1. Clone this repository to your local machine.
   ```bash
   git clone https://github.com/remla24-team3/operation.git
   cd operation
   ```
## 1. Provisioning with Vagrant and Ansible

### Start Vagrant and Provision VMs

0. Setup SSH-key
```bash
vagrant ssh-config
```

1. Create and start the Vagrant VMs:
    ```sh
    vagrant up
    ```

## 2. Build and Use Local Docker Images with Minikube

### Switch to Minikube's Docker Daemon

1. Evaluate Minikube's Docker environment:
    ```sh
    eval $(minikube -p minikube docker-env)
    ```

2. To start the application, use the following Docker Compose command:
   ```bash
   docker-compose up --build
   ```

## 3. Apply Kubernetes Manifests

### TODO: Install Prometheus Operator

### Apply Your Kubernetes Manifests

1. Apply the updated service manifest:
    ```sh
    kubectl apply -f kubernetes/service.yaml
    ```

2. Apply the other Kubernetes manifests:
    ```sh
    kubectl apply -f kubernetes/deployment.yaml
    kubectl apply -f kubernetes/ingress.yaml
    kubectl apply -f kubernetes/servicemonitor.yaml
    kubectl apply -f kubernetes/prometheusrule.yaml
    ```

## 4. Verify Setup

### Verify that all resources are created successfully

1. Get pods:
    ```sh
    kubectl get pods
    ```

2. Get services:
    ```sh
    kubectl get services
    ```

3. Get ingress:
    ```sh
    kubectl get ingress
    ```

4. Get ServiceMonitors:
    ```sh
    kubectl get servicemonitors
    ```

5. Get PrometheusRules:
    ```sh
    kubectl get prometheusrules
    ```


This will build and start all the services defined in the `compose.yaml`, which include:

- `model-service`: Backend service handling machine learning operations.
- `app-frontend`: Frontend interface for interacting with the application.
- `app-service`: Backend service that handles business logic and interacts with the model-service.

The `app-frontend` can be viewed [locally](http://localhost:3000/).

### Configuration Files

- `.dvc/config`: Configuration for data version control, pointing to a Google Drive remote for large data and model files.
- `compose.yaml`: Defines the services and their configuration necessary to run the application.

## Assignment Progress Log

### Assignment A1
We implemented the subtasks: 
- Poetry package management
- Remote data storage
- DVC Pipeline
- DVC Metrics
- Pylint & Flake 8 for code quality part of Workflow

Tag: https://github.com/jasperbruin/remla-ML-group3/releases/tag/a1

### Assignment A2

Significant progress has been made across various repositories:

- **Model-Training**: Enhanced the training pipeline from A1 with automated linters for code quality, integrating GitHub Actions for continuous integration.
- **Model-Service**: Set up a Docker container to serve the ML model via a Flask API, ensuring the model can be queried independently. Implemented CI/CD pipelines for automated deployment.
- **Lib-ML**: Extended the library to include preprocessing logic, which is used both in model-training and model-service, released via PyPi for easy dependency management.
- **Lib-Version**: Developed a version-aware utility to manage and report versions within the app-service.
- **App**: A Dockerized web application built with React.js for the frontend and Flask for the backend.
- **Operation**: Established as the central repository for deployment and operation, including Docker Compose files for easy startup and README.md for detailed documentation.

Tag: https://github.com/remla24-team3/operation/releases/tag/a2 

## Contact

For more information or support, please open an issue in this repository or contact one of the team members directly through GitHub.
