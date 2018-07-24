pipeline {
  agent {
    node{
      label 'jenkins_hk'
    }
  }
  options {
    skipDefaultCheckout(true)
  }

  
  stages {
    stage('Check Language Version') {
      post {
        always {
          dingTalk accessToken: 'ccf14be7b8173ca4f3adb8531916fc37355f6921b3c58655cde7356279a273ea',
           imageUrl: 'https://www.iconsdb.com/icons/preview/orange/info-2-xxl.png',
           jenkinsUrl: 'https://jenkins.mobi.me',
           message: '  Pipeline start..  ',
           notifyPeople: '13761247272'
          }
      }
      steps {
        checkout([$class: 'GitSCM', 
                    branches: [[name: '*/release']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [[$class: 'SubmoduleOption', 
                                  disableSubmodules: false, 
                                  parentCredentials: true, 
                                  recursiveSubmodules: true, 
                                  reference: '', 
                                  trackingSubmodules: false]], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[credentialsId: 'd0f6a358-6f2e-4f11-823b-b0c31838f942', 
                                         url: 'https://github.com/mobiwallet/mobi-card.git']]]) 
        nodejs('node10.1.0') {
          sh 'apk --no-cache add curl'
          sh 'npm --version'
          sh 'node --version'
          sh 'echo $PROJECT_NAME'
        }

      }
    }
    stage("submodule process") {
      steps {
        echo "ignore"

      }
    }
    stage('Build According BranchName') {
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

    stage('create staging deployment') {
      when {
              // case insensitive regular expression for truthy values
              expression { env.BRANCH_NAME == 'master' }
          }
      steps {
        timeout(time: 30, unit: 'SECONDS') {
           input 'Are you sure to deploy?'
        }
        echo 'create codedeployment from deployment group in aws'
        withEnv(overrides: ['PROJECT_NAME=\'txgh-test\'']) {
          sh "echo $PROJECT_NAME"
          step([$class: 'AWSCodeDeployPublisher',
                          applicationName: 'MOBI-Staging',
                          awsAccessKey: '',
                          awsSecretKey: '',
                          credentials: 'Staging',
                          deploymentGroupAppspec: true,
                          deploymentGroupName: 'txgh-test',
                          deploymentMethod: 'deploy',
                          iamRoleArn: '',
                          includes: '**',
                          excludes: '.node_modules/',
                          proxyHost: '',
                          proxyPort: 0,
                          region: 'cn-north-1',
                          s3bucket: 'jenkinscicode',
                          s3prefix: 'CodeDeploy/txgh-test',
                          subdirectory: '',
                          versionFileName: '',
                          waitForCompletion: true])
        }

      }
    }

    stage('create production deployment') {
      when {
              // case insensitive regular expression for truthy values
              expression { env.BRANCH_NAME == 'develop' }
          }
      steps {
        input 'Are you sure to deploy?'
        echo 'create codedeployment from deployment group in aws'
        withEnv(overrides: ['PROJECT_NAME=\'txgh-test\'']) {
          sh "echo $PROJECT_NAME"
          step([$class: 'AWSCodeDeployPublisher',
                          applicationName: 'MOBI-Staging',
                          awsAccessKey: '',
                          awsSecretKey: '',
                          credentials: 'Staging',
                          deploymentGroupAppspec: true,
                          deploymentGroupName: 'txgh-test',
                          deploymentMethod: 'deploy',
                          iamRoleArn: '',
                          includes: '**',
                          excludes: '.node_modules/',
                          proxyHost: '',
                          proxyPort: 0,
                          region: 'cn-north-1',
                          s3bucket: 'jenkinscicode',
                          s3prefix: 'CodeDeploy/txgh-test',
                          subdirectory: '',
                          versionFileName: '',
                          waitForCompletion: true])
        }

      }
    } //stage
    stage('Cleanup') {
      steps {
        echo 'test'
      }
    }// stage

  }  //stages

  post {

    always {
        echo "One way or another, I have finished and clean up"
        deleteDir()
      }

    aborted {
       dingTalk accessToken: 'ccf14be7b8173ca4f3adb8531916fc37355f6921b3c58655cde7356279a273ea',
        imageUrl: 'https://www.iconsdb.com/icons/preview/orange/info-2-xxl.png',
        jenkinsUrl: 'https://jenkins.mobi.me',
        message: '  Build Aborted! $Author ',
        notifyPeople: '13761247272'
    }
    fixed {
       dingTalk accessToken: 'ccf14be7b8173ca4f3adb8531916fc37355f6921b3c58655cde7356279a273ea',
        imageUrl: 'https://www.iconsdb.com/icons/preview/orange/info-2-xxl.png',
        jenkinsUrl: 'https://jenkins.mobi.me',
        message: '  Build Fixed!  ',
        notifyPeople: '13761247272'
      }
    success {
       dingTalk accessToken: 'ccf14be7b8173ca4f3adb8531916fc37355f6921b3c58655cde7356279a273ea',
        imageUrl: 'https://www.iconsdb.com/icons/preview/royal-blue/check-mark-11-xxl.png',
        jenkinsUrl: 'https://jenkins.mobi.me',
        message: '  Pipeline Success!  ',
        notifyPeople: '13761247272'
      }
    unstable {
       dingTalk accessToken: 'ccf14be7b8173ca4f3adb8531916fc37355f6921b3c58655cde7356279a273ea',
        imageUrl: 'https://www.iconsdb.com/icons/preview/orange/info-2-xxl.png',
        jenkinsUrl: 'https://jenkins.mobi.me',
        message: '  Pipeline unstable!  ',
        notifyPeople: '13761247272'
      }
    changed {
       dingTalk accessToken: 'ccf14be7b8173ca4f3adb8531916fc37355f6921b3c58655cde7356279a273ea',
        imageUrl: 'https://www.iconsdb.com/icons/preview/orange/info-2-xxl.png',
        jenkinsUrl: 'https://jenkins.mobi.me',
        message: '  Pipeline changed!  ',
        notifyPeople: '13761247272'
      }
    failure {
       dingTalk accessToken: 'ccf14be7b8173ca4f3adb8531916fc37355f6921b3c58655cde7356279a273ea',
        imageUrl: 'https://www.iconsdb.com/icons/preview/soylent-red/x-mark-3-xxl.png',
        jenkinsUrl: 'https://jenkins.mobi.me',
        message: '  Pipeline failure!  ',
        notifyPeople: '13761247272'
      }
  } //post




  environment {
    Author = 'Vance Li'
  }
}
