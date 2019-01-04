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
          app = docker.build("rahulqelfo/result") 
             } 
          sh 'docker build -t rahulqelfo/result ./result'
      }
    } 
    stage('Build vote') {
      steps {
        sh 'docker build -t rahulqelfo/vote ./vote'
      }
    }
    stage('Build worker') {
      steps {
        sh 'docker build -t rahulqelfo/worker ./worker'
      }
    }
    stage('Push result image') {
      steps {
        script {
			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
			        app.push("${BUILD_NUMBER}")
			            app.push("latest")
			        }
      }
    }
    stage('Push vote image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'rahulqelfo', url:'') {
          sh 'docker push rahulqelfo/vote'
        }
      }
    }
    stage('Push worker image') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry(credentialsId: 'rahulqelfo', url:'') {
          sh 'docker push rahulqelfo/worker'
        }
      }
    }
  }
}
