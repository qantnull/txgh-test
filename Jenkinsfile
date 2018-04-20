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
        sh '''python --version
echo "awscli needed"'''
      }
    }
    stage('error') {
      steps {
        listAWSAccounts()
        awsIdentity()
      }
    }
  }
  environment {
    Author = 'Vance Li'
  }
}