pipeline {
    agent any

    environment {
        IMAGE_NAME = 'your-dockerhub-username/mlops-a1'  // Change this to your DockerHub username
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $IMAGE_NAME:latest .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://index.docker.io/v1/']) {
                        sh 'docker push $IMAGE_NAME:latest'
                    }
                }
            }
        }

        stage('Deploy Notification') {
            steps {
                mail to: 'admin@example.com',
                    subject: 'Deployment Successful',
                    body: 'The latest Docker image has been deployed successfully!'
            }
        }
    }
}
