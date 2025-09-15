pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-django-app'
        CONTAINER_NAME = 'my-django-container'
        HOST_PORT = '8080'
        CONTAINER_PORT = '8000' // Django default
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/PresAndreichev/my-django-devops-project.git',
                    branch: 'main',
                    credentialsId: 'my-github-credentials' // if private repo
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Remove old image/container if exists
                    sh """
                    docker rm -f ${CONTAINER_NAME} || true
                    docker rmi -f ${IMAGE_NAME} || true
                    """

                    // Build the Docker image
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Run the container
                    sh """
                    docker run -d --name ${CONTAINER_NAME} -p ${HOST_PORT}:${CONTAINER_PORT} ${IMAGE_NAME}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Django app deployed! Access it at http://localhost:${HOST_PORT}"
        }
        failure {
            echo "Pipeline failed. Check the logs."
        }
    }
}
