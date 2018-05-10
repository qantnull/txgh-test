pipeline {
  environment {
    Author = 'Vance Li'
  }
  
  
  agent {
    docker {
      image 'node:9.11-alpine'
      args '-v /var/lib/jenkins:/opt/awsconfig'
    }
  }
  
  stages {
    stage('Check Language Version') {
      steps {
                nodejs(nodeJSInstallationName: 'node10.1.0') {
                sh 'npm --version'
                sh 'node --version'
                sh 'echo $PROJECT_NAME'
           }
      }
    }
    
    stage('Build According BranchName'){
      steps {
                 sh  """ 
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
 
    stage('create deployment') {
      steps {
        echo 'create codedeployment from deployment group in aws'
        
        withEnv(['PROJECT_NAME=\'txgh-test\'']){
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
  }

}
