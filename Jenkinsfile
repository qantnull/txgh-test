pipeline {
  agent {
    docker {
      image 'node:9.11-alpine'
    }
    
  }
  stages {
    stage('install requirements') {
      steps {
        sh 'pwd;ls;pip install -r requirements.txt'
      }
    }
    stage('package codes') {
      steps {
        sh '''python --version
echo "awscli needed"'''
      }
    }
  }
  environment {
    Author = 'Vance Li'
  }
}