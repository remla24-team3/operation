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
We implemented the subtasks: 
- Poetry package management
- Remote data storage
- DVC Pipeline
- DVC Metrics
- Pylint & Flake 8 for code quality part of Workflow

Tag: https://github.com/jasperbruin/remla-ML-group3/releases/tag/a1

### Assignment A2

In this phase, we achieved the following milestones:

- **Containerization and Orchestration**: Implemented Docker Compose to facilitate easy deployment of the application components including the app-frontend, app-service, and model-service.
- **Operational Documentation**: Updated the `README.md` to include comprehensive documentation on system operation, configuration details, and interaction with the Docker Compose setup.
- **Inter-service Communication**: Ensured that the app-frontend communicates only with the app-service and not directly with the model-service to adhere to architectural guidelines and prevent cross-domain request issues.
- **Repository Management**: Established and maintained public repositories under the `remla24-team3` GitHub organization to ensure transparency and accessibility of the codebase for peer and examiner review.
- **Continuous Integration**: Integrated GitHub Actions to automatically build and deploy services upon each commit, enhancing the robustness and reliability of the deployment pipeline.

Tag:

## Contact

For more information or support, please open an issue in this repository or contact one of the team members directly through GitHub.
