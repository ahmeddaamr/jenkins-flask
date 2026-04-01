pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ahmedamr25/flask-app"
        DOCKER_TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    app = docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {
                        app.push()
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
