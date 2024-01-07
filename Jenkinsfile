pipeline {
    agent any
   
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('dockerhub')
        DOCKER_IMAGE_NAME = 'devops'
        DOCKER_IMAGE_TAG = 'latest'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Assuming this is a Node.js application, install dependencies
                    sh 'npm install'
                }
            }
        }

        stage('Build and Push Image') {
            steps {
                script {
                    // Build Docker image
                    def dockerImage = docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}")

                    // Log in to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CREDENTIALS) {
                        // Tag the image for Docker Hub
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
