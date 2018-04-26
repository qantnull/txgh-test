pipeline {
  agent {
    docker {
      image 'node:9.11-alpine'
    }
  }
  
  stages {
    stage('create deployment') {
        steps {
          echo "create codedeployment from deployment group in aws"
          step([$class: 'AWSCodeDeployPublisher', \
                applicationName: "MOBI-Staging", \
                awsAccessKey: '', awsSecretKey: '', credentials: "Staging", \
                deploymentGroupAppspec: false, \
                deploymentGroupName: "txgh-test", \
                deploymentMethod: 'deploy', \
                excludes: '', \
                iamRoleArn: '', \
                includes: '**', \
                proxyHost: '', \
                proxyPort: 0, \
                region: 'ap-northeast-1', \
                s3bucket: "circleci-code", \
                s3prefix: 'mobi-admin-00247b6ea8.zip', \
                subdirectory: 'mobi-admin-00247b6ea8.zip', \
                versionFileName: '', \
                waitForCompletion: true])
        }
      }
  }
  environment {
    Author = 'Vance Li'
  }
}
