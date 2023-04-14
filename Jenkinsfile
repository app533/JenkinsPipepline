pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('fodocker')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t tmujee200/DockerFile .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-alladin 098'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push tmujee200/DockerFile'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
