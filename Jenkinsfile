pipeline {
    agent any
    stages { 	
        stage('Build Image') {
            steps {
                script {
                	app = docker.build("rahulqelfo/result")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
			        	app.push("${BUILD_NUMBER}")
			            app.push("latest")
			        }
                }
            }
        }        
    }
}
