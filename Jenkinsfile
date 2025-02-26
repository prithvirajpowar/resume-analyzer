pipeline {
    agent any

    environment {
        IMAGE_NAME = "resume-analyzer"
        CONTAINER_NAME = "resume-analyzer-container"
        DOCKER_HUB_USER = "prithvirajpowar"
    }

    stages {
        stage('Build Spring Boot Application') {
            steps {
                script {
                    sh 'ls -la'  // Check files in workspace
                    sh 'cd backend/resume-analyzer/demo && mvn clean package -DskipTests'
                }
            }
        }
    }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Run Application with Docker') {
            steps {
                script {
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"
                    sh "docker run -d --name ${CONTAINER_NAME} -p 8080:8080 ${IMAGE_NAME}:latest"
                }
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful!'
        }
        failure {
            echo 'Build Failed! Check logs for errors.'
        }
    }
}
