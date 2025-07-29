pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'Docker-Creds'
        DOCKER_IMAGE = "komall6/node-bulletin-board"
        DOCKER_TAG = "latest"
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
