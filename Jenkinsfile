pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/piyushprasad8122-creator/django-todo-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t todo-app .
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                docker stop todo-app-container || true
                docker rm todo-app-container || true

                docker run -d \
                  --name todo-app-container \
                  -p 8000:8000 \
                  todo-app
                '''
            }
        }
    }
}
