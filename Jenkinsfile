pipeline {
  agent {
    docker {
      image 'python'
    }
    
  }
  stages {
    stage('install requirements') {
      steps {
        sh 'whoami;pip install -r requirements.txt'
      }
    }
    stage('package codes') {
      steps {
        sh '''python --version
echo "awscli needed"'''
      }
    }
  }
  environment {
    Name = 'Vance Li'
  }
}