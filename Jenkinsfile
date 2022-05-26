pipeline {
  agent any
  stages{
    stage('Docker Build'){
      steps{
        sh 'docker-compse -f docker-compose.yml up -d'
        sh 'slepp 30'
      }
    }

    stage('Build & Push Docker images') {
      when {
        branch 'development'
        }
      steps{
        sh '''
        $(aws ecr get-login --no-include-email --region eu-west-1)
        docker build -t "${ECR_REPO_PHP}":"${GIT_COMMIT}" -f docker/php/test/Dockerfile .
        docker push "${ECR_REPO_PHP}":"${GIT_COMMIT}"
        docker build -t "${ECR_REPO_NGINX}":"${GIT_COMMIT}" -f docker/nginx/test/Dockerfile .
        docker push "${ECR_REPO_NGINX}":"${GIT_COMMIT}"
        '''
        }
      }
    }
}
