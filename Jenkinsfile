pipeline {
  agent {
    node {
      label 'docker'
    }
  }
  stages {
    stage('Build result') {
      steps {
        sh 'docker build -t registry.hub.docker.com/rahulqelfo/result ./result'
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
          sh 'docker push rahulqelfo/result'
        }
}
      }
    }
    stage('Push vote image') {
      steps {
          withDockerRegistry(credentialsId: 'dockerhub', url:'https://registry.hub.docker.com') {
          sh 'docker push rahulqelfo/vote'
        }
      }
    }
    stage('Push worker image') {
      steps {
        withDockerRegistry(credentialsId: 'dockerhub', url:'https://registry.hub.docker.com') {
          sh 'docker push rahulqelfo/worker'
        }
      }
    }
  }
}

