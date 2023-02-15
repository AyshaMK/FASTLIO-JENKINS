pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhubaccount')
    }
  stages {
    stage('Checkout') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: '*/main']],
          userRemoteConfigs: [[url: 'https://github.com/AyshaMK/FASTLIO-JENKINS']]
        ])
      }
    }
    
    stage('Build') {
    steps {
    sh 'docker build -t mkaysha/fastlio-jenkins .'
    }
    }
   stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
     stage('Push') {
      steps {
        sh 'docker push mkaysha/fastlio-jenkins'
      }
    }
    
  }
  post {
    always {
    sh 'docker logout'
    }
    }
}

