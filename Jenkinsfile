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
      parallel {
        stage('package codes') {
          steps {
            sh '''node --version
apk add --update python python-dev py-pip build-base
pip install awscli  '''
          }
        }
        stage('') {
          steps {
            listAWSAccounts()
          }
        }
      }
    }
    stage('error') {
      steps {
        sh '''pwd
ls
whoami
env
'''
        s3FindFiles(bucket: 'circleci-code', path: 'mobi-admin-00247b6ea8.zip')
        s3Download(file: 'mobi-admin-00247b6ea8.zip', bucket: 'circleci-code', path: 'mobi-admin-00247b6ea8.zip')
      }
    }
    stage('show aws identity') {
      steps {
        listAWSAccounts()
        s3FindFiles(path: 'mobi-admin-00247b6ea8.zip', bucket: 'circleci-code')
      }
    }
  }
  environment {
    Author = 'Vance Li'
  }
}