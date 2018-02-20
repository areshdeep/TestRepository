pipeline {
	agent any
    stages {
    	stage('Cleanup'){
                steps{
                    cleanWs()
                }
        }
        stage('CheckOut'){
            steps {
                echo 'CheckOut code'
                git url: 'https://github.com/areshdeep/TestRepository'
            }
        }
        stage('Build') {
            steps {
                echo 'Build code'
                build 'JenkinsMySample'
            }
        }
	    stage('Testing') {
			steps {
				echo 'Testing..'
			}
		}
		stage('Deploy') {
			steps {
				echo 'Deploy..'
			}
		} 
	   
	    stage('SonarQube analysis') {
			steps {
				echo 'Sonar Qube analysis..'
			}
		}
	}
}
