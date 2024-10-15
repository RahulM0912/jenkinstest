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
            agent any
            steps {
                echo 'Starting to push the image'
                withCredentials([usernamePassword(credentialsId: 'kaiser126-dockerhub', passwordVariable: 'DOCKERHUB_TOKEN', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    sh "docker login -u kiaser126 -p dckr_pat_srnty2J6H1hUxJLiiwasKMXWUdw "
                    sh ' docker push kiaser126/junkinstest:latest '
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
