# Django Todo App – CI/CD Pipeline with Jenkins & Docker

This repository demonstrates a **production-style CI/CD pipeline** built using **Jenkins** and **Docker** for a Django Todo application.  
The project focuses on automating build, deployment, health checks, and failure notifications using industry best practices.

---

## 🚀 Project Overview

The CI/CD pipeline automatically:

- Pulls code from GitHub
- Builds a Docker image for the Django application
- Runs database migrations inside the container
- Deploys the application using Docker
- Performs an application health check
- Sends **email notifications on pipeline failure**

This project is designed to showcase **real-world DevOps workflows**, not just basic automation.

---

## 🧰 Tech Stack

- **Application**: Django 3.2
- **CI/CD**: Jenkins (Declarative Pipeline)
- **Containerization**: Docker
- **Version Control**: Git & GitHub
- **Notifications**: Jenkins Email Extension (Gmail SMTP)
- **OS / Platform**: Ubuntu (AWS EC2)

---

## 📂 Repository Structure


.
├── Dockerfile
├── Jenkinsfile
├── manage.py
├── requirements.txt
├── todos/
├── templates/
└── README.md


---

## ⚙️ Jenkins Pipeline Stages

### 1. Checkout Code
- Fetches the `develop` branch from GitHub.

### 2. Build Docker Image
- Builds a Docker image using Python 3.9 for Django compatibility.

### 3. Deploy Application
- Stops and removes any existing container.
- Runs a new container on port `8000`.

### 4. Health Check
- Waits for the application to start.
- Validates application availability using HTTP status codes (2xx–3xx).
- Fails the pipeline if the application is unreachable.

### 5. Failure Notification
- Sends an email alert when the pipeline fails.
- Includes job name, build number, and console log URL for quick debugging.

---

## 📧 Email Notification Details

- Implemented using **Jenkins Email Extension Plugin**
- Gmail SMTP configured with **App Password**
- Notifications trigger **only on pipeline failure**
- Sender identity configured via Jenkins system settings

This ensures fast visibility and reliable alerting.

---

## 🧪 Failure Testing Strategy

Pipeline failure alerts were tested using **controlled failure scenarios**, such as:
- Forcing health check failure
- Simulating Docker build errors

This approach validates alerting without breaking application logic.

---

## 🧠 Key Learnings

- End-to-end CI/CD automation using Jenkins
- Docker image lifecycle management
- Safe container redeployment without port conflicts
- Health checks as deployment gates
- SMTP authentication and email troubleshooting in Jenkins
- Debugging real CI/CD pipeline failures

---

## 🔮 Future Enhancements

- Slack notifications
- Multibranch Jenkins pipeline
- Docker image push to Docker Hub
- Separate staging and production environments
- Automated test integration

---

## 👤 Author

**Piyush Prasad**  
Aspiring DevOps / Cloud Engineer  

- GitHub: https://github.com/piyushprasad8122-creator  
- LinkedIn: https://www.linkedin.com/in/ppiy  

---

## ⭐ Note

This project reflects **practical DevOps experience**, including troubleshooting, optimization, and documentation of real CI/CD challenges
