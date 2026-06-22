# 🚀 Tomato Food Delivery Application - DevOps CI/CD Deployment on AWS EKS

## 📌 Project Overview

This project demonstrates the deployment of a containerized MERN-based Food Delivery Application using modern DevOps practices and AWS Cloud services.

The application consists of:

* Frontend Application (Customer Portal)
* Admin Dashboard
* Backend API Service
* MongoDB Atlas Database

The entire deployment is automated using Jenkins CI/CD Pipeline and deployed on Amazon EKS (Elastic Kubernetes Service).

---

# 🏗️ Architecture

```text
GitHub
   │
   ▼
Jenkins CI/CD Pipeline
   │
   ├── SonarQube Code Analysis
   ├── Trivy Security Scan
   ├── Docker Build
   ├── Push Images to Amazon ECR
   └── Deploy to Amazon EKS
            │
            ▼
      Kubernetes Cluster
            │
   ┌────────┼────────┐
   │        │        │
Frontend  Backend  Admin
   │        │        │
   └────────┼────────┘
            │
      MongoDB Atlas
```

---

# 🛠️ Technologies Used

## Cloud Services

* AWS EC2
* AWS EKS
* AWS ECR
* AWS IAM
* AWS VPC
* AWS Load Balancer

## DevOps Tools

* Jenkins
* Docker
* Kubernetes
* Amazon EKS
* Amazon ECR
* SonarQube
* Trivy
* Git
* GitHub

## Application Stack

### Frontend

* React.js
* Vite
* Nginx

### Backend

* Node.js
* Express.js

### Database

* MongoDB Atlas

---

# 📂 Project Structure

```text
DevOps-Project-04
│
├── admin/
├── backend/
├── frontend/
│
├── k8s/
│   ├── admin-deployment.yaml
│   ├── admin-service.yaml
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── frontend-deployment.yaml
│   ├── frontend-service.yaml
│   ├── secrets.yaml
│
├── Jenkinsfile
├── docker-compose.yaml
├── README.md
```

---

# 🐳 Docker Implementation

Each component is containerized using Docker.

### Docker Images

* tomato-backend
* tomato-frontend
* tomato-admin

Images are built automatically through Jenkins and pushed to Amazon ECR.

---

# ☸️ Kubernetes Deployment

The application is deployed using Kubernetes manifests.

### Deployments

* backend-deployment
* frontend-deployment
* admin-deployment

### Services

| Service  | Type         |
| -------- | ------------ |
| Frontend | LoadBalancer |
| Admin    | LoadBalancer |
| Backend  | ClusterIP    |

---

# 🔒 Security Implementation

## SonarQube

Integrated SonarQube for:

* Static Code Analysis
* Code Smell Detection
* Quality Gate Validation

### Quality Gate Status

✅ Passed

---

## Trivy

Integrated Trivy for:

### Filesystem Scan

```bash
trivy fs .
```

### Docker Image Scan

```bash
trivy image tomato-backend
trivy image tomato-frontend
trivy image tomato-admin
```

---

# 📦 Amazon ECR

Docker images are stored in:

* tomato-backend
* tomato-frontend
* tomato-admin

Repository Region:

```text
ap-south-1
```

---

# ☁️ Amazon EKS

Cluster Name:

```text
tomato-eks
```

Node Group:

```text
tomato-nodes
```

Instance Type:

```text
t3.small
```

Region:

```text
ap-south-1
```

---

# ⚙️ Jenkins CI/CD Pipeline

Pipeline Stages:

```text
1. Checkout Source Code
2. SonarQube Analysis
3. Trivy File Scan
4. Build Backend Docker Image
5. Build Frontend Docker Image
6. Build Admin Docker Image
7. Trivy Image Scan
8. Login to Amazon ECR
9. Tag Docker Images
10. Push Images to ECR
11. Update Kubeconfig
12. Deploy to Amazon EKS
13. Verify Deployment
```

---

# 🚀 Deployment Process

## Clone Repository

```bash
git clone https://github.com/akashak0717/DevOps-Project-04.git
```

## Build Docker Images

```bash
docker build -t tomato-backend ./backend

docker build -t tomato-frontend ./frontend

docker build -t tomato-admin ./admin
```

## Push to ECR

```bash
docker push <ECR-REPOSITORY>
```

## Deploy to Kubernetes

```bash
kubectl apply -f k8s/
```

## Verify Deployment

```bash
kubectl get pods

kubectl get svc
```

---

# 📊 Project Outcomes

✅ Containerized MERN Application

✅ Dockerized Frontend, Backend and Admin

✅ Automated CI/CD Pipeline using Jenkins

✅ Integrated SonarQube Code Quality Checks

✅ Integrated Trivy Security Scanning

✅ Hosted Docker Images in Amazon ECR

✅ Deployed Application on Amazon EKS

✅ Exposed Applications through AWS Load Balancers

✅ Implemented Kubernetes Deployments and Services

---

# 🎯 Learning Outcomes

Through this project I gained hands-on experience in:

* Docker Containerization
* Kubernetes Orchestration
* Amazon EKS
* Amazon ECR
* Jenkins CI/CD
* SonarQube
* Trivy
* IAM Roles and Policies
* Kubernetes Services and Deployments
* Production-grade DevOps Workflow

---

# 👨‍💻 Author

Akash Aralikatti

GitHub:
https://github.com/akashak0717

LinkedIn:
https://www.linkedin.com/in/akasharalikatti0717/

---

# ⭐ If you found this project useful, please give it a star.