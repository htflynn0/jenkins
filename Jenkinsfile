pipeline{
	agent any 
	stages{
		stage('Build'){
			steps{
				echo 'Build'
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