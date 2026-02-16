Django Todo App – CI/CD with Jenkins & Docker
📌 Project Overview

This project demonstrates a complete CI/CD pipeline for a Django Todo application using:

GitHub for source code management

Jenkins for Continuous Integration

Docker for containerization

Ubuntu (AWS EC2) as the deployment environment

The goal of this project is to build, containerize, and deploy a Django application automatically using Jenkins, while handling real-world CI/CD issues and fixing them step by step.

🛠️ Tech Stack

OS: Ubuntu (AWS EC2)

Language: Python

Framework: Django 3.2

CI Tool: Jenkins (installed via Snap)

Containerization: Docker & Docker Compose

Version Control: Git & GitHub

🏗️ Project Structure
django-todo-cicd/
├── Dockerfile
├── docker-compose.yml
├── manage.py
├── todoApp/
├── todos/
├── staticfiles/
└── README.md
🚀 What I Built

Jenkins job that:

Pulls code from GitHub

Builds a Docker image

Runs Django inside a container

Fully automated build process

CI-safe container handling (no port conflicts)

❌ Problems Faced & How I Fixed Them

This project involved real CI/CD troubleshooting. Below are the actual problems I faced and how I resolved them.

1️⃣ Jenkins Could Not Use Docker

Problem
Jenkins builds were failing when running Docker commands.

Reason
Jenkins was installed via Snap, which:

Does not create a jenkins Linux user

Has restricted access to Docker socket by default

Fix

sudo chmod 666 /var/run/docker.sock
sudo systemctl restart docker
sudo systemctl restart snap.jenkins.jenkins

This allowed Jenkins to communicate with Docker.

2️⃣ Docker Build Failed – distutils Module Missing

Error

ModuleNotFoundError: No module named 'distutils'

Reason

Dockerfile was using python:3

python:3 pulled Python 3.12

Django 3.2 is not compatible with Python 3.12

Fix
Pinned Python version in Dockerfile:

FROM python:3.9

Python 3.9 is fully compatible with Django 3.2.

3️⃣ Jenkins Could Not Find Dockerfile or docker-compose.yml

Error

no configuration file provided: not found

Reason
Jenkins runs builds inside its own workspace, not the home directory.

Fix

Configured Jenkins Source Code Management (Git)

Ensured the repository is cloned into Jenkins workspace

Ran Docker commands from the correct directory

4️⃣ Git Push Failed – Branch Mismatch

Error

error: src refspec develop does not match any

Reason

Commit was made on main

Tried to push to develop

Fix

git push origin main
5️⃣ Docker Container Failed – Port 8000 Already in Use

Error

Bind for 0.0.0.0:8000 failed: port is already allocated

Reason

Jenkins job started a new container on every build

Old containers were never stopped

Port 8000 was already occupied

Fix (CI-safe & professional solution)
Updated Jenkins Execute shell step:

set -e

docker stop todo-app-container || true
docker rm todo-app-container || true

docker build . -t todo-app

docker run -d \
  --name todo-app-container \
  -p 8000:8000 \
  todo-app

This ensures:

Old containers are removed

Port conflicts never occur

Builds are repeatable and stable

✅ Final CI/CD Workflow

Developer pushes code to GitHub

Jenkins pulls the latest code

Docker image is built

Old container is removed

New container is deployed

Django app runs successfully

🌐 Accessing the Application

Once the Jenkins build is SUCCESS, access the app using:

http://<EC2-PUBLIC-IP>:8000
📚 Key Learnings

Jenkins Snap vs APT differences

Docker permission management

Importance of pinning runtime versions

Jenkins workspace vs local filesystem

CI-safe container lifecycle management

Real-world debugging using Jenkins Console Output

📌 Why This Project Matters

This project is not a simple tutorial.
It reflects real DevOps work, including:

Debugging CI failures

Fixing dependency issues

Handling Docker & Jenkins integration

Writing production-safe CI scripts

🔮 Future Improvements

Convert Freestyle job to Jenkins Pipeline (Jenkinsfile)

Add GitHub Webhook for auto-build

Use Docker Compose for multi-container setup

Deploy to cloud using Nginx + Gunicorn

👤 Author

Piyush Prasad
GitHub: https://github.com/piyushprasad8122-creator
