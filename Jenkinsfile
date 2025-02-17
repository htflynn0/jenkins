pipeline{
	// agent any 
	agent {
		docker{
			image 'maven:3.6.3'
		}
	}
	stages{
		stage('Build'){
			steps{
				echo 'Build'
				echo 'mvn --version'
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