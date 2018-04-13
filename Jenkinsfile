pipeline {
  agent {
    docker {
      image 'python'
    }
    
  }
  stages {
    stage('install requirements') {
      steps {
        sh 'pip install -r requirements'
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