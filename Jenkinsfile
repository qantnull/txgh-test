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

        withAWS(profile:'default') {
          s3Upload(file:'/root/testjenkinsupload', bucket:'circleci-code', path:'test/')
        }
      }
    }
  }
  environment {
    Author = 'Vance Li'
  }
}
