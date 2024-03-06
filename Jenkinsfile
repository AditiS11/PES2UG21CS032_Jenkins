pipeline {
	agent {
		docker {
			image 'node:14'
		}
	}
	stages {
		stage('Clone repository') {
			steps {
				script {
					git branch: 'main',
					url: 'https://github.com/AditiS11/PES2UG21CS032_Jenkins.git'
				}
			}
		}
		stage('Install Dependencies') {
			steps {
				script {
					sh 'npm install'
				}
			}
		}
		stage('Build Application') {
			steps {
				script {
					sh 'npm run build'
				}
			}
		}
		stage('Test Application') {
			steps {
				script {
					sh 'npm test'
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					sh 'docker build -t AditiS11/Image1:$BUILD_NUMBER .'
					sh 'docker push AditiS11/Image1:$BUILD_NUMBER'
				}
			}
		}
	}
	post {
		always {
			script {
				currentBuild.result = currentBuild.result ?: 'SUCCESS'
				if (currentBuild.result != 'SUCCESS') {
					echo 'Pipeline failed'
				}
			}
		}
	}
}
