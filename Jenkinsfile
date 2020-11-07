pipeline {
  agent any
  environment {
    registry = "isieiam/se_crawler"
    VERSION = '1.0'
    dockerImage = ''
    registryCredential = 'dockerhub_id'
  }
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$VERSION" 
        }
      }
    }
  stage('Test') {
      steps{
        script {
          sh '''echo "some tests"'''
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }

        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:${VERSION}"
      }
    }
  }
}
