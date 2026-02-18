pipeline {
    agent any

    environment {
        APP_NAME = "todo-app"
        CONTAINER_NAME = "todo-app-container"
        APP_PORT = "8000"
        EMAIL_TO = "piyushprasad8122@gmail.com"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'develop',
                    url: 'https://github.com/piyushprasad8122-creator/django-todo-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $APP_NAME .'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true

                docker run -d \
                  --name $CONTAINER_NAME \
                  -p $APP_PORT:$APP_PORT \
                  $APP_NAME
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                echo "Waiting for application to start..."
                sleep 10

                STATUS_CODE=$(curl -o /dev/null -s -w "%{http_code}" http://localhost:9999)

                if [ "$STATUS_CODE" -lt 200 ] || [ "$STATUS_CODE" -ge 400 ]; then
                  echo "Health check failed with status code: $STATUS_CODE"
                  exit 1
                fi

                echo "Health check passed with status code: $STATUS_CODE"
                '''
            }
        }
    }

    post {
        failure {
            emailext(
                to: "${EMAIL_TO}",
                subject: "❌ Jenkins FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hello,

Your Jenkins pipeline has FAILED.

Job Name: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Status: FAILURE

Failed Stage:
${env.STAGE_NAME}

Error:
${currentBuild.currentResult}

Console Log:
${env.BUILD_URL}console

Regards,
Jenkins
"""
            )
        }
    }
}
