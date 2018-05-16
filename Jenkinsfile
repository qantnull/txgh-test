pipeline {
  agent {
    docker {
      image 'node:9.11-alpine'
      args '-v /var/lib/jenkins:/opt/awsconfig'
    }
  }
  
  stages {
    stage('Check Language Version') {
      steps {
        checkout([$class: 'GitSCM', 
                  branches: [[name: '*/develop']], 
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

        sh 'cd src/'
        git credentialsId: 'd0f6a358-6f2e-4f11-823b-b0c31838f942', url: 'https://github.com/mobiwallet/mobi-app-localization.git'
        sh 'cd ../'
        
        nodejs('node10.1.0') {
          sh 'apk --no-cache add curl'
          sh 'npm --version'
          sh 'node --version'
          sh 'echo $PROJECT_NAME'
        }

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
                          waitForCompletion: false])
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
                          waitForCompletion: false])
        }

      }
    } //stage
    stage('Cleanup') {
      steps {
          sh """ 
              curl -XPOST https://oapi.dingtalk.com/robot/send?access_token=$DToken \
                -H "Content-Type: application/json" \
                -d "{
                        'msgtype': 'markdown',
                        'markdown': {
                            'title': '$JOB_NAME deployed successfully',
                            'text': '### **$JOB_NAME** deployed \n\n> **$JOB_NAME**\n'
                        }
                    }"
          """
      }
    }// stage

  }  //stages
  
  environment {
    Author = 'Vance Li'
  }
}
