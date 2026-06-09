pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t django-app:v1 .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f django-container || true
                docker run -d --name django-container -p 8000:8000 django-app:v1
                '''
            }
        }

    }
}
