pipeline {
    agent any

    environment {
        IMAGE_NAME = 'arun256docker/fastapi-app'
        DOCKER_CREDENTIALS_ID = 'dockerhub-creds'
        DOCKER_TAG = "latest" // You can use build number or git hash here for versioning
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Arun256-git/Python_FastAPI_Cloud.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image: ${IMAGE_NAME}:${DOCKER_TAG}"
                    dockerImage = docker.build("${IMAGE_NAME}:${DOCKER_TAG}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    echo "Pushing Docker image to Docker Hub..."
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Clean Up Local Image') {
            steps {
                script {
                    echo "Cleaning up local Docker image..."
                    sh "docker rmi ${IMAGE_NAME}:${DOCKER_TAG} || true"
                }
            }
        }

        stage('Deploy (Optional)') {
            when {
                expression { return false } // Change to true if deployment is configured
            }
            steps {
                echo 'Deployment logic goes here (e.g., Docker run, SSH to server, kubectl apply)'
            }
        }
    }

    post {
        always {
            echo '✅ Jenkins pipeline finished.'
        }
        failure {
            echo '❌ Jenkins pipeline failed.'
        }
    }
}
