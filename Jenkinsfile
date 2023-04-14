node {   
    stage('Clone repository') {
        git credentialsId: 'GitHub', url: 'https://github.com/app533/JenkinsPipepline'
    }
    
    stage('Build image') {
       dockerImage = docker.build("tmujee200/DockerFile")
    }
    
 stage('Push image') {
        withDockerRegistry([ credentialsId: "fordocker", url: "" ]) {
        dockerImage.push()
        }
    }    
}
