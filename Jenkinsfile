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
apk add --update python python-dev py-pip build-base
pip install awscli  '''
      }
    }
    stage('error') {
      steps {
        sh '''aws configure list 
s3FindFiles bucket: \'circleci-code\', path: \'mobi-admin-00247b6ea8.zip\'
'''
      }
    }
    stage('show aws identity') {
      steps {
        listAWSAccounts()
      }
    }
  }
  environment {
    Author = 'Vance Li'
  }
}