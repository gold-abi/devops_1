pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/gold-abi/devops_1.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t quote-generator:latest .
                '''
            }
        }

        stage('Deploy Locally (Run Container)') {
            steps {
                sh '''
                # Stop and remove old container if it exists
                docker rm -f quote-site || true

                # Run new container from latest image
                docker run -d \
                  --name quote-site \
                  -p 8081:80 \
                  quote-generator:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'Application successfully deployed locally on http://localhost:8081'
        }
        failure {
            echo 'Pipeline failed. Check build or deployment logs.'
        }
    }
}
