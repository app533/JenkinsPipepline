pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('fordocker')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t  tmujee200/dockerfile:CWpoveimage . '
      }
    }
    stage('Checkout') {
       steps {
      git 'https://github.com/app533/foronar.git'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Test') {
       steps {
              sh 'docker run --rm tmujee200/dockerfile echo "Container lau"'
            }
        }

    stage('Push') {
      steps {
        sh 'docker push tmujee200/dockerfile'
      }
    }
    stage('Futher Testing with SonarQube Scanner') {
      steps {
        withSonarQubeEnv('SonarQube') {
         sh 'sonar-scanner -D"sonar.projectKey=server.js" -D"sonar.sources=." -D"sonar.host.url=http://3.226.235.109:9000" -D"sonar.token=squ_2c262fa80555964eb9c30656a5f74c7512f10e26"'
        }
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
  
}
