pipeline {
  agent any
  environment {
    registry = "isieiam/se_crawler"
    registryCredential = 'dockerhub_id'
    dockerImage = ''
    VERSION = '1.0'
  }
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":${VERSION}"
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
