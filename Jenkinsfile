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

                docker run -d \
                    --name django-container \
                    -p 8000:8000 \
                    -v django_data:/app \
                    django-app:v1

                sleep 10

                docker exec django-container python manage.py migrate

                curl http://localhost:8000
                '''
            }
        }
    }
}
