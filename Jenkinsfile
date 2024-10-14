pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhubcredentials') // Adjust with your credentials ID
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
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
