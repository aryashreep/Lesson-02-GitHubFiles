node {
    def newApp
    def registry = 'aryashreep/simplilearn-devops-certification'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/valera-rozuvan/online-counter.git'
	}
	stage('Build') {
		sh 'echo "I am inside the container"'
	}
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Registring image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
