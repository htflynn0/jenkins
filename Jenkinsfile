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
				sh 'maven --version'
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
		stage('Test'){
			steps{
				echo 'Test'
			}
		}
		stage('Intergration Test'){
			steps{
				echo 'Intergration Test'
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