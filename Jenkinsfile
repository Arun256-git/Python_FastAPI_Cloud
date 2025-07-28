pipeline {
    agent any

    environment {
        IMAGE_NAME = 'arun256docker/fastapi-app'
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
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                    script {
                        docker.image("${IMAGE_NAME}").push('latest')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment logic goes here (e.g., kubectl, SSH, etc.)'
            }
        }
    }
}
