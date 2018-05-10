pipeline {
  agent {
    docker {
      image 'node:9.11-alpine'
      args '-v /var/lib/jenkins:/opt/awsconfig'
    }

  }
  stages {
    stage('Build') {
      steps {
                nodejs(nodeJSInstallationName: 'node10.1.0') {
                sh 'npm --version'
                sh 'node --version'
           }
      }
    }
 
    stage('create deployment') {
      steps {
        echo 'create codedeployment from deployment group in aws'
        step([$class: 'AWSCodeDeployPublisher', 
              applicationName: 'MOBI-Staging', 
              awsAccessKey: '', 
              awsSecretKey: '', 
              credentials: 'Staging', 
              deploymentGroupAppspec: true, 
              deploymentGroupName: 'txgh-test', 
              deploymentMethod: 'deploy', 
              excludes: '.node_modules', 
              iamRoleArn: '', 
              includes: '**', 
              proxyHost: '', 
              proxyPort: 0, 
              region: 'cn-north-1', 
              s3bucket: 'jenkinscicode', 
              s3prefix: 'CodeDeploy/txgh-test', 
              subdirectory: '', versionFileName: '', 
              waitForCompletion: false])
      }
    }
  }
  environment {
    Author = 'Vance Li'
  }
}
