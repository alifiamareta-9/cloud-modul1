pipeline {
    agent any
    environment {
        IMAGE_NAME = 'alifiamareta9/simple-app'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials'
        DOCKER_PATH = 'C:\\Users\\Alifia Mareta\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Build di Windows"
            }
        }
        stage('Build Docker Image') {
            steps {
                bat '"%DOCKER_PATH%" build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: env.REGISTRY_CREDENTIALS,
                    usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat '"%DOCKER_PATH%" login -u %USER% -p %PASS%'
                    bat '"%DOCKER_PATH%" push %IMAGE_NAME%:%BUILD_NUMBER%'
                }
            }
        }
    }
}
