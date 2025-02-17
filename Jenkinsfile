pipeline{
	agent any 
	environment{
		dockerHome = tool "myDocker"
		mavenHome = tool "myMaven"
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	// agent {
	// 	// docker{
	// 	// 	image 'maven:3.6.3'
	// 	// }
	// 	docker{
	// 		image 'node:21.7'
	// 	}
	// }
	stages{
		stage('Build'){
			steps{
				sh 'mvn --version'
				sh 'docker --version'
				echo 'Build'
				echo "Path: $PATH"
				echo "Build Number: $env.BUILD_NUMBER"
				echo "Build ID: $env.BUILD_ID"
				echo "Build tag: $env.BUILD_TAG"
				echo "Build URL: $env.BUILD_URL"
				echo "Job name: $env.JOB_NAME"
			}
			post{
				always{
					echo 'I run at the end of the build stage'
				}
			}
		}
		stage('Complie'){
			steps{
				sh "mvn clean compile"
			}
		}
		stage('Test'){
			steps{
				echo 'mvn test'
			}
		}
		stage('Intergration Test'){
			steps{
				echo 'Intergration Test'
			}
		}
		stage('Package'){
			steps{
				sh "mvn package -DskippTests"
			}
		}
		stage('Build docker image'){
			steps{
				// docker build -t htflynn/currency-exchange-devops:$env.BUILD_TAG
				script{
					// docker build -t htflynn/currency-exchange-devops:$env.BUILD_TAG
					set DOCKER_HOST=tcp://localhost:2375

					dockerImage = docker.build("htflynn/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push docker image'){
			steps{
				script{
					docker.withRegistry('', 'dockerhub'){
						dockerImage.push()
						dockerImage.push('latest')
					}
					
				}
			}
		}
	}
	post {
		always{
			echo 'I always run'
		}
		success{
			echo 'I run when successful'
		}
		failure{
			echo 'I run when failed'
		}
	}
}