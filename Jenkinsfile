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
          //sh "docker build -t ${registry}:${VERSION} ."
          dockerImage = docker.build registry + ":$VERSION" 
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          //withCredentials([usernamePassword(credentialsId: 'dockerhub_id', passwordVariable: 'pass', usernameVariable: 'user')]) {
            //sh '''
            //      echo "$pass" | docker login --username $user --password-stdin
            //      docker push ${registry}:${VERSION}
            //   '''
          //}
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
