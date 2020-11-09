pipeline { 
    environment { 
        registry = "aryashreep/simplilearn-devops-certification" 
        registryCredential = 'docker-hub-credentials' 
        dockerImage = '' 
    }
    agent any 
    stages { 
        stage('Cloning our Git') { 
            steps { 
                git 'https://github.com/aryashreep/simplilearn-devops-certification.git' 
            }
        } 
        stage('Building our image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        }
        stage('Deploy our image') { 
            steps { 
                script {
                    sh "docker rmi --force $registry:$BUILD_NUMBER"
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        } 
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi --force $registry:$BUILD_NUMBER" 
            }
        } 
    }
}
node {
    stage('Execute Image'){
        def customImage = docker.build("aryashreep/simplilearn-devops-certification:${env.BUILD_NUMBER}")
        customImage.inside {
            sh 'echo This is the code executing inside the container.'
        }
    }
}
