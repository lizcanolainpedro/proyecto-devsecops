pipeline {
    agent any

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t app-vulnerable .'
            }
        }

        stage('Security Scan') {
            steps {
                sh '''
                docker run --rm \
                -v /var/run/docker.sock:/var/run/docker.sock \
                ghcr.io/aquasecurity/trivy:latest \
                image --exit-code 1 --severity CRITICAL,HIGH app-vulnerable
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Desplegando aplicación...'
            }
        }
    }
}
