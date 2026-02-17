pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'develop',
                    url: 'https://github.com/piyushprasad8122-creator/django-todo-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t todo-app .'
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

        stage('Health Check') {
            steps {
                sh '''
                echo "Waiting for application to start..."
                sleep 10

                STATUS_CODE=$(curl -o /dev/null -s -w "%{http_code}" http://localhost:8000)

                if [ "$STATUS_CODE" -ne 200 ]; then
                  echo "Health check failed. App is not responding."
                  exit 1
                fi

                echo "Health check passed. App is live."
                '''
            }
        }
    }
}
