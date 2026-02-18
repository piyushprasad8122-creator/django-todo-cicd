🚀 Django Todo App – CI/CD with Jenkins & Docker

This project demonstrates a complete CI/CD pipeline using Jenkins, Docker, and GitHub to build, deploy, monitor, and notify failures for a Django-based Todo application.

It is designed as a learning + resume-ready DevOps project covering real-world CI/CD practices.

📌 Project Overview

The pipeline automatically performs the following actions whenever code is pushed to the repository:

Pulls source code from GitHub

Builds a Docker image for the Django application

Runs database migrations inside the container

Deploys the application using Docker

Performs a health check on the running application

Sends an email notification if the pipeline fails

🧱 Tech Stack

Backend: Django 3.2

CI/CD: Jenkins (Declarative Pipeline)

Containerization: Docker

Source Control: Git & GitHub

Notifications: Jenkins Email Extension (Gmail SMTP)

OS: Ubuntu (EC2)

📂 Repository Structure
.
├── Dockerfile
├── Jenkinsfile
├── manage.py
├── requirements.txt
├── todos/
├── templates/
└── README.md
🔧 Jenkins Pipeline Stages
1️⃣ Checkout Code

Pulls the develop branch from GitHub.

2️⃣ Build Docker Image

Builds a Docker image using python:3.9 for Django compatibility.

3️⃣ Deploy Application

Stops and removes any existing container.

Runs a new container on port 8000.

4️⃣ Health Check

Waits for the application to start.

Validates the app using HTTP status codes (2xx–3xx).

Fails the pipeline if the app is unreachable.

5️⃣ Email Notification (on Failure)

Sends a detailed email when the pipeline fails.

Includes job name, build number, and console log link.

📜 Jenkinsfile (Key Features)

Declarative pipeline syntax

Safe container redeployment (no port conflicts)

Controlled health check logic

Email alerts using emailext

Clear failure reporting

📧 Email Notification Setup

Email alerts are configured using:

Email Extension Plugin

Gmail SMTP with App Password

Notifications are triggered only on pipeline failure

This ensures quick visibility and faster debugging.

🧪 How Failure Testing Was Done

To test alerting without breaking production code:

Health check was temporarily pointed to an invalid port

Pipeline failed gracefully

Email alert was successfully triggered

This simulates real-world failure scenarios safely.

🧠 Key Learnings

End-to-end CI/CD automation with Jenkins

Docker image lifecycle management

Handling port conflicts in deployments

Health checks as deployment gates

SMTP and Jenkins email troubleshooting

Debugging real pipeline failures

📈 Future Improvements

Add Slack notifications

Convert to Multibranch Pipeline

Push Docker images to Docker Hub

Add staging & production environments

Integrate automated tests

👤 Author

Piyush Prasad
Aspiring DevOps / Cloud Engineer

GitHub: https://github.com/piyushprasad8122-creator

LinkedIn: https://www.linkedin.com/in/ppiy
