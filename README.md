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

### Local development

1. Start minikube + apply all yaml files
```bash
   minikube stop
   minikube delete
   minikube start
   minikube dashboard
```

1. Install helm
   
   ```bash
   helm install monitoring prom-repo/kube-prometheus-stack -n monitoring --create-namespace
   
   helm repo add istio https://istio-release.storage.googleapis.com/charts
   helm repo update
   helm install istio-base istio/base -n istio-system --create-namespace
   helm install istiod istio/istiod -n istio-system
   helm install istio-ingress istio/gateway -n istio-system

   kubectl apply -f kubernetes/app-frontend.yaml
   kubectl apply -f kubernetes/app-service.yaml
   kubectl apply -f kubernetes/app-service-v2.yaml
   kubectl apply -f kubernetes/model-service.yaml
   kubectl apply -f kubernetes/gateway.yaml
   kubectl apply -f kubernetes/virtualservices.yaml
   kubectl apply -f kubernetes/service-account.yaml -n monitoring
   kubectl apply -f kubernetes/monitoring-service.yaml -n monitoring
   ```
2. Start tunnel (maybe require sudo rights)
   ```bash
   sudo minikube tunnel
   ```
3. Enable Ingress
   ```bash
   minikube addons enable ingress
   ```
   
4. Test Prometheus 
   ```bash
   kubectl port-forward svc/myprom-kube-prometheus-sta-prometheus 9090:9090
   ```

5. **Retrieve Admin Password**:
    ```bash
    kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
    ```

6. **Configure Prometheus Data Source**:
    - Go to the Grafana configuration page.
    - Add Prometheus as a data source with URL `http://prometheus-server.monitoring.svc.cluster.local:9090`.

7. **Import Grafana Dashboard**:
    - Use the Grafana UI to import the provided JSON dashboard definition.
    - Select the Prometheus data source and import the dashboard.

### Start Vagrant and Provision VMs

2. Setup SSH-key
```bash
vagrant ssh-config
```

3. Create and start the Vagrant VMs:
 ```sh
 vagrant up
 ```

 ```sh
vagrant ssh controller
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

### Assignment A3

#### Setting up (Virtual) Infrastructure
- **Automated Configuration**: We used a loop and template arithmetic in our configuration scripts to define node names and IPs dynamically. This approach helps streamline the setup process for multiple nodes.
- **Vagrant Compatibility**: **A note of caution: Vagrant seems to only work reliably on our Apple computers, and there might be compatibility issues on other systems.**

#### Setting up Software Environment
- **Prometheus, Grafana, and Kubernetes Dashboard**: These monitoring and management tools are now directly reachable once the environment is set up. This simplifies the monitoring and management of our Kubernetes cluster.

#### Kubernetes Usage
- **Application Deployment**: The application can now be deployed to a Kubernetes cluster. The deployment files include a Deployment, a Service, and an Ingress configuration.
- **Ingress Controller**: The app is accessible through the Ingress controller, eliminating the need to open a node port or tunnel a service.
- **Docker Compatibility Issues**: We encountered issues running Docker containers due to ARM vs AMD architecture differences. As a result, the correctness of our Ingress settings is still under review and will be addressed in the upcoming weeks.

#### App Monitoring
- **Basic Metrics**: The application successfully launches, but we acknowledge the need to add more detailed metrics to monitor various aspects of the application's performance.

#### Grafana
- **Dashboard Configuration**: The project includes a JSON definition for a basic Grafana dashboard. This dashboard can be imported to visualize app-specific metrics.
- **Documentation**: The operations repository's README.md now contains instructions for manually installing the Grafana dashboard, ensuring users can set it up correctly.

- Tag: https://github.com/remla24-team3/operation/releases/tag/a3

### Assignment A4

#### ML Testing

- **Pytest**: Add Pytest in model training
- **Tests**: Feature and Data, Model development and Model infrastructure
- **Tests**: Memory and Performance
- **Tests**: Mutamorphic
- **Tests**: Non-determinism robustness and model capabilities through data slices
- **Frontend**:Improvements in app

- Tag: https://github.com/remla24-team3/operation/releases/tag/a4

## Contact

For more information or support, please open an issue in this repository or contact one of the team members directly through GitHub.
