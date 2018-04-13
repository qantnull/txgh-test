pipeline {
  agent {
    docker {
      image 'alpine:3.7'
    }
    
  }
  stages {
    stage('Output Test') {
      parallel {
        stage('Output Test') {
          steps {
            echo 'hello'
          }
        }
        stage('') {
          steps {
            echo 'jenkins'
          }
        }
      }
    }
  }
}