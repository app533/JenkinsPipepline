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
    stage('Clone sources') {
            steps {
                git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/app533/javapro.git'
            }
        }
   stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner -D"sonar.projectKey=wq" -D"sonar.sources=./server.js" -D"sonar.host.url=http://44.200.247.190:9000" -D"sonar.token=squ_d76b31314fbc0462219b77b36f2a13f48e3e4498"'
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
