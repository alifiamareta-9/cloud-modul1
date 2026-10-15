pipeline {
    agent any
    environment {
        IMAGE_NAME = 'alifiamareta9/simple-app'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials'
        DOCKER_PATH = 'C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe'
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
                bat '"' + env.DOCKER_PATH + '" build -t ' + env.IMAGE_NAME + ':' + env.BUILD_NUMBER + ' .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: env.REGISTRY_CREDENTIALS,
                    usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat '"' + env.DOCKER_PATH + '" login -u %USER% -p %PASS%'
                    bat '"' + env.DOCKER_PATH + '" push ' + env.IMAGE_NAME + ':' + env.BUILD_NUMBER
                }
            }
        }
    }
}
