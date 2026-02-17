stage('Health Check') {
    steps {
        sh '''
        echo "Waiting for application to start..."
        sleep 10

        STATUS_CODE=$(curl -o /dev/null -s -w "%{http_code}" http://localhost:8000)

        if [ "$STATUS_CODE" -ge 200 ] && [ "$STATUS_CODE" -lt 400 ]; then
          echo "Health check passed with status $STATUS_CODE"
        else
          echo "Health check failed with status $STATUS_CODE"
          exit 1
        fi
        '''
    }
}
