pipeline {
    agent any

    environment {
        IMAGE_NAME = 'vivek-web'
        CONTAINER_NAME = 'vivek-web'
        HOST_PORT = '8081'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker rm -f ${CONTAINER_NAME} 2>/dev/null || true
                    docker run -d --name ${CONTAINER_NAME} -p ${HOST_PORT}:80 ${IMAGE_NAME}:latest
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    docker ps --filter name=${CONTAINER_NAME}
                    curl -f http://localhost:${HOST_PORT}
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD deployment completed successfully.'
        }
        failure {
            echo 'CI/CD pipeline failed. Check the stage logs above.'
        }
    }
}
