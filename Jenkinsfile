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
        stage('error') {
          steps {
            echo 'jenkins'
          }
        }
      }
    }
    stage('') {
      steps {
        sh 'uname -a; pwd;ls'
      }
    }
  }
  environment {
    Name = 'Vance Li'
  }
}