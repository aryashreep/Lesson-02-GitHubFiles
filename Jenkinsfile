pipeline {
  environment {
    registry = "aryashreep/simplilearn-devops-certification"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/valera-rozuvan/online-counter.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Execute Image'){
        def customImage = docker.build("aryashreep/simplilearn-devops-certification:${env.BUILD_NUMBER}")
        customImage.inside {
            sh 'echo This is the code executing inside the container.'
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
        sh "docker rmi -f $registry:$BUILD_NUMBER"
      }
    }
  }
}
