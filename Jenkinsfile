pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'anhhao2004'
        IMAGE_NAME = "${DOCKER_REGISTRY}/nextjs-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest", '.')
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'dockerhub-credentials', url: '']) {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }

        stage('Notify/Deploy') {
            steps {
                echo "Image ${IMAGE_NAME}:latest pushed to Docker Hub"
                // Gửi webhook cho ArgoCD hoặc trigger deploy tại đây nếu cần
            }
        }
    }
}
