pipeline {
    agent {
        docker {
            image 'docker:stable'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhubcredentials') // Adjust with your credentials ID
        IMAGE_NAME = 'kiaser126/junkinstest' // Docker Hub repo name
        IMAGE_TAG = 'latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/RahulM0912/jenkinstest.git', branch: 'main'
                echo 'Git Checkout completed'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
                echo 'Build Image Completed'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                echo 'Login Completed'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                sh 'docker push ${IMAGE_NAME}:${IMAGE_TAG}'
                echo 'Push Image Completed'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
