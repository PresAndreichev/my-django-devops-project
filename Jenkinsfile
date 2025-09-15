pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/PresAndreichev/my-django-devops-project.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                // Now you're in a Git directory
                sh 'git remote -v'
            }
        }
    }
}
