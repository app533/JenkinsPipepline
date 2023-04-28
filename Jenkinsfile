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
                    sh 'sonar-scanner -D"sonar.projectKey=Server.js_project" -D"sonar.sources=./server.js" -D"sonar.host.url=http://3.234.251.90:9000" -D"sonar.token=squ_194df50934a51ecb9227fe2545bb42d3ec1e8a9d"'
                 }
            }
        }
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
          sh 'kubectl run nodejs0 --image=tmujee200/dockerfile'
        } 
      }
      stage('deployment Nodejs'){
        steps{
         sh 'kubectl create deployment nodejs0 --image=gcr.io/google-samples/nodejs0:v1'
        }
        }
      stage('to scale the application'){
        steps{
         // sh 'kubectl scale deployments/ nodejs0 --replicas=4'
            sh 'kubectl scale deployments/nodejs0 --replicas=4'
        }
        }
//       stage('Kubernetes Pods and Nodes'){
//         steps{
//            sh  'kubectl exec nodejs11 -- env'
//         }
//       }
//       stage('create container '){
//         steps{
//           sh 'kubectl exec -it nodejs11 -- bash'
//         } 
//       }
//       stage('Check APP Runing '){
//         steps{
//           sh 'curl localhost:8080'
//         }
//       }
      
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
//            steps{
//                 sshagent(['123']) {
//                   sh 'kubectl run testing12 --image=tmujee200/dockerfile'
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

