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
    stage('show env') {
      steps {
        sh '''node --version
apk add --update python python-dev py-pip build-base
pip install awscli  
pwd
ls
whoami
env
aws configure list'''
      }
    }
    stage('show aws') {
      steps {
        sh 'echo $AWS_SECRET_ACCESS_KEY'
        s3Download(file: 'mobi-admin-00247b6ea8.zip', bucket: 'circleci-code', path: 'mobi-admin-00247b6ea8.zip')
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