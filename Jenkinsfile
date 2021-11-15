pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="413752907951"
        AWS_DEFAULT_REGION="us-east-2" 
        IMAGE_REPO_NAME="space-registry"
        IMAGE_TAG="latest"
        REPOSITORY_URI ="${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
    }
     
    node {
    def app

    stage('Clone repository') {
        git branch: "master", url: "git@github.com:/lordkroft/space.git", credentialsId: "lordkroft"
    }

    stage('Build image') {
        sh "docker build --build-arg APP_NAME=flask -t ${REPOSITORY_URI}:${IMAGE_TAG} -f Dockerfile ."
    }

    stage('Push image') {
        docker.withRegistry('https://${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com', 'ecr:${AWS_DEFAULT_REGION}:lordkroft') {
            sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/space-registry:${IMAGE_TAG}"
        }
    }
  }
}
