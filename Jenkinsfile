pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="413752907951"
        AWS_DEFAULT_REGION="us-east-2" 
        IMAGE_REPO_NAME="space-registry"
        IMAGE_TAG="latest"
        REPOSITORY_URI ="${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
    }
    
    stages {

        stage('Cloning Git') {
            steps {
                git branch: "master", url: "git@github.com:/lordkroft/space.git", credentialsId: "lordkroft"
    }
            }
        }

    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}"
        }
      }
    }

    // Uploading Docker images into AWS ECR
    stage('Pushing to ECR') {
     steps{
         script {
                docker.withRegistry('https://${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com', 'ecr:${AWS_DEFAULT_REGION}:lordkroft') {
            sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/space-registry:${IMAGE_TAG}"
         }
        }
      }
    }
}
