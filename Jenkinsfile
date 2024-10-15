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
                withCredentials([usernamePassword(credentialsId: 'kaiser126-dockerhub', passwordVariable: 'DOCKERHUB_TOKEN', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    // Using --password-stdin to securely log in to Docker
                    sh 'echo $DOCKERHUB_TOKEN | docker login -u $DOCKERHUB_USERNAME --password-stdin'
                    sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
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
