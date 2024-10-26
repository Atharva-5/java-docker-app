pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('d935a6f9-4227-4272-be8e-18e237109a8c')  // Define your Docker Hub credentials in Jenkins
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
                bat 'mvn clean package' // Use 'bat' for Windows
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    bat "docker build -t atharva0507/java-docker-app:latest ." // Use 'bat' for Windows
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Log in to Docker Hub
                    bat "echo d935a6f9-4227-4272-be8e-18e237109a8c | docker login -u atharva0507 --password-stdin" // Use 'bat' for Windows

                    // Push the Docker image to Docker Hub
                    bat "docker push atharva0507/java-docker-app :latest" // Use 'bat' for Windows
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images after the build
            bat "docker rmi atharva0507/java-docker-app :latest" // Use 'bat' for Windows
        }
    }
}
