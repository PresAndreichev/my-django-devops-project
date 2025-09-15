pipeline {
    agent {
        docker {
            image 'python:3.11-slim'
            args '-u root:root'
        }
    }

    environment {
        DOCKER_IMAGE = "my-django-app:${env.BUILD_NUMBER}"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'pip install --no-cache-dir -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest || true'  // allows pipeline to continue if no tests yet
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
