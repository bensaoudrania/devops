pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'dockerhub'
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
                    // Log in to Docker Hub using Jenkins credentials
                    withCredentials([usernamePassword(credentialsId: DOCKER_HUB_CREDENTIALS,
                                                     usernameVariable: 'DOCKERHUB_USER',
                                                     passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                        // Build Docker image
                        sh "docker build -t ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ."
                       
                        // Log in to Docker Hub
                        sh "docker login -u ${DOCKERHUB_USER} -p ${DOCKERHUB_PASSWORD}"
                       
                        // Tag the image for Docker Hub
                        sh "docker tag ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ${DOCKERHUB_USER}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
                       
                        // Push the image to Docker Hub
                        sh "docker push ${DOCKERHUB_USER}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
                       
                        // Log out from Docker Hub
                        sh "docker logout"
                    }
                }
            }
        }
    }
}

