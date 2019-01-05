pipeline {
  agent {
    node {
      label 'docker'
    }
  }
  stages {
    stage('Build result') {
      steps {
          script {
                app1 = docker.build("pranshu2011/result", './result')
                }
      }
    } 
    stage('Build vote') {
      steps {
           script {
                app2 = docker.build("pranshu2011/vote", './vote')
                }
      }
    }
    stage('Build worker') {
      steps {
           script {
                app3 = docker.build("pranshu2011/worker", './worker')
                }
      }
    }
    stage('Push result image') {
      steps {
          script {
			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
			        app1.push("${BUILD_NUMBER}")
			            app1.push("latest")
			        }
                }
      }
    }
    stage('Push vote image') {
      steps {
      script {
			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
			        app2.push("${BUILD_NUMBER}")
			            app2.push("latest")
			        }
                }
      }
    }
    stage('Push worker image') {
      steps {
         script {
			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
			        app3.push("${BUILD_NUMBER}")
			            app3.push("latest")
			        }
                }
      }
    }
  }
}
