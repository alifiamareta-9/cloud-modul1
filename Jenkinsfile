stage('Build Docker Image') {
    steps {
        bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
    }
}
stage('Push Docker Image') {
    steps {
        withCredentials([usernamePassword(credentialsId: REGISTRY_CREDENTIALS,
            usernameVariable: 'USER', passwordVariable: 'PASS')]) {
            bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" login -u %USER% -p %PASS%'
            bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" push %IMAGE_NAME%:%BUILD_NUMBER%'
        }
    }
}
