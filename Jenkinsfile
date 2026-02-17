pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t todo-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop todo-app-container || true
                docker rm todo-app-container || true
                docker run -d --name todo-app-container -p 8000:8000 todo-app
                '''
            }
        }
    }
}
