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
    stage('Futher Testing with SonarQube Scanner') {
      steps {
        withSonarQubeEnv('SonarQube') {
         echo "Scanning with SonarQube" 
//          sh 'sonar-scanner -D"sonar.projectKey=newpro" -D"sonar.sources=." -D"sonar.host.url=http://3.226.235.109:9000" -D"sonar.token=squ_0b45e114e48b33c1f97bdd57e5dd7255cb37b953"'
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
