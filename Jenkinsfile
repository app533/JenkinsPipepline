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
   stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('SonarQube') {
          echo "weqwee"
         sh sonar-scanner \
         -Dsonar.projectKey=ok21 \
         -Dsonar.sources=.\server.js \
         -Dsonar.host.url=http://44.202.233.71:9000 \
         -Dsonar.token=squ_81228677b80d1564f95398257263e0077befadd4
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
