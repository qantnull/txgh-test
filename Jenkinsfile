pipeline {
  agent {
    docker {
      image 'node:9.11-alpine'
    }
    
  }
  stages {
    stage('install requirements') {
      steps {
        sh 'echo "npm install"'
      }
    }
    stage('package codes') {
      steps {
        sh '''node --version
echo "awscli needed"'''
      }
    }
    stage('error') {
      steps {
        awsIdentity()
      }
    }
  }
  environment {
    Author = 'Vance Li'
  }
}