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
                sh 'docker build -t quote-generator:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f quote-site || true
                docker run -d -p 8081:80 --name quote-site quote-generator:latest
                '''
            }
        }
    }
}
