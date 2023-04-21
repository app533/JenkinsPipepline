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
         sh 'sonar-scanner -D"sonar.projectKey=neforjavapro" -D"sonar.sources=." -D"sonar.host.url=http://44.202.195.71:9000" -D"sonar.token=squ_68395f3afacdc0fdbe0a0f89c7f3983eda9745eb"'
        }
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
