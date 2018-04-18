pipeline {
  agent {
    docker {
      image 'python:3.6.4-alpine'
    }
    
  }
  stages {
    stage('install requirements') {
      steps {
        sh 'pip install -r requirements.txt'
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
    Name = 'Vance Li'
  }
}
