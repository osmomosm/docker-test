pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/osmomosm/docker-test.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t osmomosm/docker-test .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push osmomosm/docker-test:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
