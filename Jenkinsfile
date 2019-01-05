pipeline {
    agent any
    stages {
        stage('Build result') {
            steps {
                script {
                app = docker.build("rahulqelfo/result", './result')
                }
            }
        }
        stage('Push result imagee') {
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

