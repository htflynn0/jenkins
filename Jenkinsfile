pipeline {
	agent any 
	environment {
		DOCKER_HOST = "tcp://localhost:2375"
		dockerHome = tool "myDocker"
		mavenHome = tool "myMaven"
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages {
		stage('Verify Docker') {
			steps {
				bat 'docker info'  // Changed from 'sh' to 'bat' for Windows
			}
		}
		
		stage('Build') {
			steps {
				bat 'mvn --version'
				bat 'docker --version'
				echo 'Build'
				echo "Path: $PATH"
				echo "Build Number: $env.BUILD_NUMBER"
				echo "Build ID: $env.BUILD_ID"
				echo "Build tag: $env.BUILD_TAG"
				echo "Build URL: $env.BUILD_URL"
				echo "Job name: $env.JOB_NAME"
			}
			post {
				always {
					echo 'I run at the end of the build stage'
				}
			}
		}

		stage('Compile') {
			steps {
				bat "mvn clean compile"
			}
		}

		stage('Test') {
			steps {
				echo 'mvn test'
			}
		}

		stage('Integration Test') {
			steps {
				echo 'Integration Test'
			}
		}

		stage('Package') {
			steps {
				bat "mvn package -DskipTests"
			}
		}

		stage('Build docker image') {
			steps {
				script {
					dockerImage = docker.build("htflynn/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push docker image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
		}
	}

	post {
		always {
			echo 'I always run'
		}
		success {
			echo 'I run when successful'
		}
		failure {
			echo 'I run when failed'
		}
	}
}
