pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 413752907951.dkr.ecr.us-east-2.amazonaws.com
                echo 'Building..now'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
