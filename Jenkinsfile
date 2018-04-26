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
        sh """
              node --version
              apk add --update python python-dev py-pip build-base
              pip install awscli
              pwd
              ls
              whoami
              env
           """
          }
        }
    stage('build according branch') {
      steps {
        sh """ 
                if [ ${BRANCH_NAME} = 'develop' ];then
                    echo "npm run build:staging"
                fi
                if [ ${BRANCH_NAME} = 'master' ];then
                    echo "npm run build:preProduction"
                fi
                if [ ${BRANCH_NAME} = 'release' ];then
                    echo "npm run build:production"
                fi
            """
        }
      }
    stage('if build successfully, package code to s3') {
      steps {
        withAWS(profile:'Prod') {
          s3Upload(file:'.', bucket:'circleci-code', path:'JenkinsCI/${JOB_NAME}')
        }
          }
       }
    stage('create deployment') {
        steps {
          echo "create codedeployment from deployment group in aws"
        }
      }
  }
  environment {
    Author = 'Vance Li'
  }
}
