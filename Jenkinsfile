pipeline {
  agent any 
  environment {
        DOCKER_HUB_CREDENTIALS = credentials('ddockerhub')
        DOCKER_IMAGE_NAME = 'devops'
        DOCKER_IMAGE_TAG = 'latest'
    }
  stages{
    stage ('build'){
      steps{
        script{
          sh 'npm install'
        }
      }
    }
    stage('Build and Push Image') {
            steps {
                script {
                    // Pull the Docker image
                    docker.image('your_base_image:tag').pull()

                    // Build Docker image
                    docker.build("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}")

                    // Log in to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CREDENTIALS) {
                        // Tag the image for Docker Hub
                        docker.image("${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }


  }
}
