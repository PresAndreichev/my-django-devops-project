pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "my-django-app:${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/PresAndreichev/my-django-devops-project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $DOCKER_IMAGE ."
            }
        }

        stage('Deploy Container') {
            steps {
                sh "docker stop myapp || true && docker rm myapp || true"
                sh "docker run -d --name myapp -p 8000:8000 $DOCKER_IMAGE"
            }
        }
    }
}
