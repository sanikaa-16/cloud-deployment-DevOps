# Cloud Native Resource Monitoring Python App

## Overview
The **Cloud Native Resource Monitoring Python App** is a lightweight cloud-native application designed to monitor system resources such as CPU and memory utilization in real-time. Built using Python's Flask framework and the `psutil` library, this application provides valuable insights into system performance.

The application is containerized using **Docker** to ensure portability and ease of deployment across multiple environments. It is further deployed on **Amazon Elastic Kubernetes Service (EKS)**, leveraging Kubernetes for efficient resource orchestration and management.

## Features
- **Real-time Monitoring:** Displays system resource utilization, including CPU and memory usage.
- **Cloud-Native Architecture:** Designed for efficient deployment in cloud environments.
- **Containerization:** Packaged as a Docker container for portability.
- **Kubernetes Orchestration:** Managed using Amazon EKS for scalability and automation.
- **AWS Integration:** Docker images are pushed to **Amazon Elastic Container Registry (ECR)** for efficient deployment.
- **Continuous Integration & Deployment (CI/CD):** Automated builds and deployments using **Jenkins**.
- **Webhook Automation:** GitHub webhooks notify Jenkins about repository updates for seamless CI/CD.

## Technologies Used
- **Python** (Flask, `psutil`)
- **Docker** (Containerization)
- **Amazon ECR** (Container Registry)
- **Amazon EKS** (Managed Kubernetes Service)
- **Kubernetes** (Container Orchestration)
- **Jenkins** (CI/CD Automation)
- **GitHub Webhooks** (Automated Deployment Triggers)

## Prerequisites
Before setting up the project, ensure you have the following installed:
- **Docker**
- **Kubernetes CLI (`kubectl`)**
- **AWS CLI** (configured with appropriate IAM permissions)
- **Amazon EKS Cluster** (pre-configured)
- **Jenkins** (with GitHub Webhook integration)

## Setup and Deployment
### 1. Clone the Repository
```sh
$ git clone https://github.com/your-repository/cloud-native-monitoring.git
$ cd cloud-native-monitoring
```

### 2. Build and Tag Docker Image
```sh
$ docker build -t cloud-monitoring-app .
```

### 3. Push Image to Amazon ECR
```sh
$ aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <your-ecr-repository-url>
$ docker tag cloud-monitoring-app:latest <your-ecr-repository-url>/cloud-monitoring-app:latest
$ docker push <your-ecr-repository-url>/cloud-monitoring-app:latest
```

### 4. Deploy to Kubernetes (EKS)
Modify `deployment.yaml` to point to your ECR image and apply the configuration:
```sh
$ kubectl apply -f deployment.yaml
```

### 5. Verify Deployment
Check the running pods and services:
```sh
$ kubectl get pods
$ kubectl get services
```

### 6. Set Up Jenkins for CI/CD
1. Install Jenkins and required plugins (**Pipeline, GitHub Integration, Kubernetes Plugin**).
2. Configure a GitHub webhook to trigger Jenkins builds on repository updates.
3. Create a Jenkins pipeline with the following steps:
   - Pull the latest changes from GitHub.
   - Build and push the Docker image to Amazon ECR.
   - Deploy the updated image to Amazon EKS.

## Usage
Once deployed, access the monitoring dashboard via the Kubernetes service URL:
```sh
http://<your-kubernetes-service-ip>:<port>
```
This will display the real-time CPU and memory usage of the system.

## Contributing
Contributions are welcome! Feel free to submit a pull request or open an issue.

## License
This project is licensed under the **MIT License**.

## Contact
For any questions or support, reach out at sanikakamath16@gmail.com.

