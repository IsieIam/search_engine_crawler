pipeline {
  agent any
  environment {
    registry = "isieiam/se_crawler"
    VERSION = '1.0'
    dockerImage = ''
  }
  stages {
    stage('Building image') {
      steps{
        //sh "docker build -t ${registry}:${VERSION} ."
        dockerImage = docker.build registry + ":$VERSION" 
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          withCredentials([usernamePassword(credentialsId: 'dockerhub_id', passwordVariable: 'pass', usernameVariable: 'user')]) {
            sh '''
                  echo "$pass" | docker login --username $user --password-stdin
                  docker push ${registry}:${VERSION}
               '''
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
