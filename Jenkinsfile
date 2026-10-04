pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-flask-app:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f flask-app || true
                docker run -d --name flask-app -p 5000:5000 jenkins-flask-app:latest
                '''
            }
        }

        stage('Verify Application') {
            steps {
                sh 'curl -f http://localhost:5000/'
            }
        }
    }
}
