pipeline {  environment {
    registry = "aryashreep/simplilearn-devops-certification"
    registryCredential = 'dockerhub'
  }  agent any  stages {
    stage('Building image') {
      steps{
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
  }
}
