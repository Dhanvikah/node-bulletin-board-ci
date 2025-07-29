pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub-creds'
        DOCKER_IMAGE = "yourdockerhubusername/node-bulletin-board"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/dockersamples/node-bulletin-board.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo 'Deployment to Kubernetes will be handled by ArgoCD (GitOps)'
            }
        }
    }
}
