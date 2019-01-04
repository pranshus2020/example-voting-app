pipeline {
  agent {
    node {
      label 'docker'
    }
  }
  stages {
    stage('Build result') {
      steps {
          sh 'docker build -t rahulqelfo/result ./result'
		    script {
                	app1 = docker.build("rahulqelfo/result")
                }
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t rahulqelfo/vote ./vote'
		  script {
                	app2 = docker.build("rahulqelfo/vote")
                }
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t rahulqelfo/worker ./worker'
		  script {
                	app3 = docker.build("rahulqelfo/worker")
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
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
   script {
			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
			        	app2.push("${BUILD_NUMBER}")
			            app2.push("latest")
			        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
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
}
}

