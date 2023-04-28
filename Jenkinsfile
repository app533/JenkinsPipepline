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
//    stage('SonarQube Analysis') {
//             steps {
//                 withSonarQubeEnv('SonarQube') {
//                     sh 'sonar-scanner -D"sonar.projectKey=Server.js_project" -D"sonar.sources=./server.js" -D"sonar.host.url=http://44.200.247.190:9000" -D"sonar.token=squ_d76b31314fbc0462219b77b36f2a13f48e3e4498"'
//                  }
//             }
//         }
    stage('Dwonlaod MiniKube'){
      steps{
        sh 'curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64'
        sh 'chmod +x minikube'
        sh ' sudo  mv minikube /usr/local/bin/'
      }
      }
    stage('Start Minikube'){
      steps{
        sh 'minikube start'
      }
    }
      
      stage('Deploy image from DockerHub to Kubernetes'){
        steps{
          sh 'kubectl run okceck --image=tmujee200/dockerfile'
        } 
      }
//     stage('Install Minikube Stage 1'){
//       steps{
//          sh 'chmod +x minikube' 
//       }
//     }
//        stage('Install Minikube Stage 2'){
//         steps{
//           sh 'echo "admin" | sudo -S mv minikube /usr/local/bin/'
//      }
//     }
    
//     stage('Deploy on k8'){
//             steps{
//                 sshagent(['final1']) {
//                   sh "kubectl run testing12 --image=tmujee200/dockerfile"
//                   script{
//                       try{
//                             sh "ssh ubuntu@192.168.49.2:8443 kubectl apply -f ."
//                      }catch(error){
//                             sh "ssh ubuntu@192.168.49.2:8443 kubectl create -f ."
//             }
//                   }
//               }
//             }
//         }

  }
  post {
    always {
      sh 'docker logout'
    }
  }
} 

