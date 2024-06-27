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

- Vagrant
- Data Version Control (DVC)

### Running the Application

1. Clone this repository to your local machine.
   ```bash
   git clone https://github.com/remla24-team3/operation.git
   cd operation
   ```

### Download our model using DVC

1. Install DVC
   ```bash
   pipx install dvc
   ```
   
2. Pull the model and data from the remote storage
   ```bash
    dvc pull
    ```

### Start Vagrant and Provision VMs

1. Create and start the Vagrant VMs:
 ```sh
 vagrant destroy -f && vagrant up
 ```

2. Launch the vagrant controller if necessary.
 ```sh
vagrant ssh controller
 ```

This will build and start all the services defined in the `compose.yaml`, which include:

- `model-service`: Backend service handling machine learning operations.
- `app-frontend`: Frontend interface for interacting with the application.
- `app-service`: Backend service that handles business logic and interacts with the model-service.

The `app-frontend` can be viewed [application](http://192.168.56.2)

The `grafana-dashboard` can be accessed at [grafana](http://192.168.56.2/grafana)

The `kubernetes` can be accessed at [kubernetes](http://192.168.56.2/dashboard)

The `prometheus` can be accessed at [prometheus](http://192.168.56.2/prometheus/)

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

### Assignment A5

#### Istio

- **Istio**: Add Istio on local development, work in progress to have it working on Vagrant.
- **Istio**: Switched from Ingress to istio Gatewway Ingress.
- **Istio**: Added Virtual Services and Destination Rule.
- **Experiment**: Deployed a second version of app-frontend and run Istio experiment with 90/10 rule.
- **Vagrant**: Slight improvements in Vagrant setup.


## Istio Use Case: Rate Limiting

1. **Open a Shell in the Pod**:
   To execute the commands, first, you need to open a shell session inside your `sleep` pod where you will run the curl requests. Use the following command to access the shell:

   ```bash
   kubectl exec -it sleep-0 -n rate-limit -- sh
   ```

2. **Execute the HTTP Requests**:
   Once inside the shell of the `sleep` pod, run the following loop to execute 15 HTTP GET requests to the `echoserver`. This step is crucial to test the rate limiting functionality. Each request will output the HTTP status code, helping you identify when rate limiting kicks in (typically indicated by `429 Too Many Requests`).

   ```bash
   for i in $(seq 1 15); do
     curl -s -o /dev/null -w "%{http_code}\n" http://echoserver.rate-limit.svc.cluster.local
   done
   ```

   This command will output the HTTP status code for each request, allowing you to verify whether and when the rate limiting rules apply.

#### Analyzing the Results
- **HTTP 200**: Indicates a successful response from the `echoserver`.
- **HTTP 429**: Indicates that the rate limiting has been enforced.

- Tag: https://github.com/remla24-team3/operation/releases/tag/a5

### Assignment A6

#### Operation

- **Report**: Created 80% version of the report

- Tag: https://github.com/remla24-team3/operation/releases/tag/a6

#### Model-training

- **Tests**: Added metric reporting to the readme
- **Code quality** Removed unused folders and files

- Tag: https://github.com/remla24-team3/model-training/releases/tag/a6


## Contact

For more information or support, please open an issue in this repository or contact one of the team members directly through GitHub.
