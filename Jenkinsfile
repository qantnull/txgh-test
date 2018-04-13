pipeline {
  agent {
    docker {
      image 'python'
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
    stage('show sys version') {
      steps {
        sh 'uname -a; pwd;ls'
      }
    }
    stage('python version') {
      steps {
        sh 'python --version'
      }
    }
  }
  environment {
    Name = 'Vance Li'
  }
}