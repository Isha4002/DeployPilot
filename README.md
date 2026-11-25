# 🚀 DeployPilot – Automated Docker CI/CD Deployment Platform

DeployPilot is a DevOps-focused deployment platform designed to automate the process of building, pushing, and deploying containerized applications using GitHub Actions and AWS.

It demonstrates an end-to-end Docker CI/CD pipeline with automated deployment to an AWS EC2 instance.

## 🎯 Project Overview

DeployPilot automates application deployment through a CI/CD workflow.

Whenever the workflow is manually triggered, it:

1. Checks out the GitHub repository.
2. Authenticates with AWS using OpenID Connect (OIDC).
3. Builds Docker images for the frontend and backend.
4. Pushes Docker images to Amazon Elastic Container Registry (ECR).
5. Uses AWS Systems Manager (SSM) to send deployment commands to EC2.
6. Pulls the latest Docker images on EC2.
7. Restarts containers using Docker Compose.
8. Performs an application health check.

## 🏗️ Architecture

```text
             Developer
                 |
                 v
          GitHub Repository
                 |
                 v
          GitHub Actions
                 |
          AWS Authentication
               (OIDC)
                 |
          +------+------+
          |             |
          v             v
     Build Backend  Build Frontend
       Docker Image   Docker Image
          |             |
          v             v
          +------+------+
                 |
                 v
          Amazon ECR
       (Docker Registry)
                 |
                 v
          AWS Systems Manager
                 |
                 v
             AWS EC2
                 |
          Docker Compose
                 |
          +------+------+
          |             |
          v             v
       Backend       Frontend
       Container     Container
          |
          v
      Health Check
```

## 🛠️ Tech Stack

| Category | Technology |
|---|---|
| CI/CD | GitHub Actions |
| Containerization | Docker |
| Container Registry | Amazon ECR |
| Cloud Infrastructure | AWS EC2 |
| AWS Authentication | IAM + OIDC |
| Remote Deployment | AWS Systems Manager |
| Container Management | Docker Compose |
| Application | React, Node.js |
| Health Verification | HTTP health check |

## ⚙️ CI/CD Pipeline

### 1. Source Code Management
GitHub stores the application source code and CI/CD workflow.

### 2. Continuous Integration
GitHub Actions builds separate Docker images for the frontend and backend.

Images are tagged using:
- `latest`
- Git commit SHA

### 3. AWS Authentication
GitHub Actions authenticates with AWS using OIDC, avoiding long-lived AWS access keys in GitHub Secrets.

### 4. Amazon ECR
The generated Docker images are pushed to two ECR repositories:
- `interviewace-backend`
- `interviewace-frontend`

### 5. Continuous Deployment
AWS Systems Manager sends commands to the EC2 instance.

The instance:
- Authenticates with Amazon ECR.
- Pulls the latest images.
- Runs Docker Compose to update the containers.
- Executes an HTTP health check.

## ☁️ AWS Infrastructure

The project uses:

- **Amazon EC2:** Hosts the containerized application.
- **Amazon ECR:** Stores Docker images.
- **AWS IAM:** Controls permissions and roles.
- **OIDC:** Provides secure GitHub Actions authentication.
- **AWS Systems Manager:** Executes deployment commands remotely.

## 🔐 Security Implementation

- GitHub Actions uses OIDC for AWS authentication.
- IAM permissions are scoped to the required ECR repositories and EC2 deployment target.
- EC2 uses an IAM role for AWS access.
- SSH access is restricted through the EC2 security group.
- Application environment variables are stored separately from source code.

## 📊 Deployment Verification

The successful GitHub Actions workflow run demonstrates:

- Backend Docker image build and push.
- Frontend Docker image build and push.
- Successful SSM command execution.
- Successful ECR login on EC2.
- Running backend and frontend containers.
- Successful application health check.

Example health-check response:

```json
{
  "success": true,
  "message": "InterviewAce API is healthy"
}
```

## 📚 Key DevOps Concepts Learned

- CI/CD automation
- Docker image creation and tagging
- Container registries
- AWS IAM and least-privilege permissions
- GitHub Actions workflows
- OpenID Connect authentication
- AWS Systems Manager
- EC2 deployment automation
- Docker Compose
- Application health checks

## 🚀 Future Improvements

Possible future enhancements:

- Automated testing before deployment.
- Monitoring with Prometheus and Grafana.
- Infrastructure provisioning using Terraform.
- Container orchestration using Kubernetes.

## 👩‍💻 Author

**Isha Pal**

B.Tech – Information Technology

GitHub: [Isha4002](https://github.com/Isha4002)

---

*DeployPilot – Automating Docker deployments with GitHub Actions and AWS.*
