pipeline {
    agent any

    stages {

        stage('Descargar Código') {
            steps {
                echo 'Clonando repositorio...'

                git branch: 'desarrollo',
                url: 'https://github.com/lizcanolainpedro/proyecto-devsecops.git'
            }
        }

        stage('Construir Imagen Docker') {
            steps {
                echo 'Construyendo imagen Docker...'

                sh 'docker build -t mi-app-segura:latest .'
            }
        }

        stage('Análisis de Seguridad (Trivy)') {
            steps {
                echo 'Analizando vulnerabilidades...'

                sh '''
                docker run --rm \
                -v /var/run/docker.sock:/var/run/docker.sock \
                ghcr.io/aquasecurity/trivy:latest \
                image --exit-code 1 --severity HIGH,CRITICAL mi-app-segura:latest
                '''
            }
        }

        stage('Despliegue en Producción (CD)') {
            steps {
                echo 'Desplegando aplicación...'

                sh 'docker stop app-produccion || true'
                sh 'docker rm app-produccion || true'

                sh 'docker run -d --name app-produccion mi-app-segura:latest'
            }
        }
    }
}pipeline {
    agent any

    stages {

        stage('Descargar Código') {
            steps {
                echo 'Clonando repositorio...'

                git branch: 'desarrollo',
                url: 'https://github.com/lizcanolainpedro/proyecto-devsecops.git'
            }
        }

        stage('Construir Imagen Docker') {
            steps {
                echo 'Construyendo imagen Docker...'

                sh 'docker build -t mi-app-segura:latest .'
            }
        }

        stage('Análisis de Seguridad (Trivy)') {
            steps {
                echo 'Analizando vulnerabilidades...'

                sh '''
                docker run --rm \
                -v /var/run/docker.sock:/var/run/docker.sock \
                ghcr.io/aquasecurity/trivy:latest \
                image --exit-code 1 --severity HIGH,CRITICAL mi-app-segura:latest
                '''
            }
        }

        stage('Despliegue en Producción (CD)') {
            steps {
                echo 'Desplegando aplicación...'

                sh 'docker stop app-produccion || true'
                sh 'docker rm app-produccion || true'

                sh 'docker run -d --name app-produccion mi-app-segura:latest'
            }
        }
    }
}
