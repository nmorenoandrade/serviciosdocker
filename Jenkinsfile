pipeline {
    agent any

    environment {
        PATH = "C:/Program Files/Docker/Docker/resources/bin;$PATH"
    }

    tools {
        maven 'Maven3'    // Nombre EXACTO configurado en Jenkins -> Global Tool Configuration
        jdk 'Java21'      // O el que hayas configurado (ej: Java17)
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/nmorenoandrade/serviciosdocker.git', credentialsId: '000c8f33-2944-4787-bc70-ee562c16b925	'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t euraka .'
            }
        }

        stage('Docker Run') {
            steps {
                bat 'docker stop euraka || true && docker rm euraka || true'
                bat 'docker run -d -p 8761:8761 --name euraka euraka'
            }
        }
    }
}