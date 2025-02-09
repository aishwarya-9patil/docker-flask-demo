pipeline {
    agent any 
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhubID')  // Jenkins credentials ID
    }
    stages { 
        stage('Build Docker Image') {
            steps {  
                script {
                    // Tag the image with your Docker Hub username and build number
                    def imageTag = "aishwarya0909/flaskapp:${BUILD_NUMBER}"
                    sh "docker build -t ${imageTag} ."
                }
            }
        }
        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using the credentials from Jenkins
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    def imageTag = "aishwarya0909/flaskapp:${BUILD_NUMBER}"
                    sh "docker push ${imageTag}"
                }
            }
        }
    }
    post {
        always {
            // Ensure to logout of Docker Hub after the job is done
            sh 'docker logout'
        }
    }
}

