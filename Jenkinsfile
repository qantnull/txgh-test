pipeline {
  agent {
    docker {
      image 'node:9.11-alpine'
    }
    
  }
  stages {
    stage('install requirements') {
      steps {
        sh 'npm install'
      }
    }
    stage('package codes') {
      steps {
        sh '''python --version
echo "awscli needed"'''
      }
    }
    stage('') {
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