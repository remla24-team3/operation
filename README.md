# Operation Repository

## Overview

This repository is part of the REMLA24-Team3 project and serves as the central hub for running and operating the URL Phishing detection application. It contains Docker Compose configurations to facilitate easy deployment and operation of the application.

### Related Repositories

- [Model Training](https://github.com/remla24-team3/model-training)
- [Model Service](https://github.com/remla24-team3/model-service)
- [Library for Machine Learning (lib-ml)](https://github.com/remla24-team3/lib-ml)
- [Library for Versioning (lib-version)](https://github.com/remla24-team3/lib-version)
- [Application Frontend and Service](https://github.com/remla24-team3/app)

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
2. To start the application, use the following Docker Compose command:
   ```bash
   docker-compose up --build
   ```

This will build and start all the services defined in the `compose.yaml`, which include:

- `model-service`: Backend service handling machine learning operations.
- `app-frontend`: Frontend interface for interacting with the application.
- `app-service`: Backend service that handles business logic and interacts with the model-service.

### Configuration Files

- `.dvc/config`: Configuration for data version control, pointing to a Google Drive remote for large data and model files.
- `compose.yaml`: Defines the services and their configuration necessary to run the application.

## Assignment Progress Log

### Assignment A1
- Initial setup of the Docker Compose file to run the model-service, app-frontend, and app-service.
- Creation of the initial README to document basic setup and operation instructions.

### Assignment A2 (current)
- Expanded the README to include detailed startup instructions and a comprehensive list of related repositories.

## Usage Notes

- The Docker Compose file is designed to be simple to use for demonstration purposes and may not reflect the full complexity needed for scalable production deployment.
- Future updates will include provisioning and deployment configurations using Vagrant, Ansible, Kubernetes, etc., to support more complex deployment scenarios.

## Contact

For more information or support, please open an issue in this repository or contact one of the team members directly through GitHub.
