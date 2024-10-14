pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('kaiser126-dockerhub') // Docker Hub token
        IMAGE_NAME = 'kiaser126/junkinstest' // Docker Hub repo name
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Build image') {
            steps {
                echo 'Starting to build docker image'
                script {
                    def customImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push Image') {
            steps {
                echo 'Starting to push the image'
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        customImage.push()
                    }
                }
            }
        }
    }
    
    post {
        always {
            sh 'docker logout'
        }
    }
}
