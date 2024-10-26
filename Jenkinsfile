pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')  // Define your Docker Hub credentials in Jenkins
        IMAGE_NAME = 'atharva0507/java-docker-app'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone the repository
                git 'https://github.com/Atharva-5/java-docker-app.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                // Build the Java application using Maven
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t ${IMAGE_NAME}:latest .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Log in to Docker Hub
                    sh 'echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin'

                    // Push the Docker image to Docker Hub
                    sh 'docker push ${IMAGE_NAME}:latest'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images after the build
            sh 'docker rmi ${IMAGE_NAME}:latest'
        }
    }
}
