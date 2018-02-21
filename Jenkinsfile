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
                echo 'Build code 1'
				bat "\"D:\\Work\\PPL\\Own\\Jenkinsetup\\nuget.exe\" restore \"${WORKSPACE}\\SampleJenkins\\SampleApp.sln\""
				script {
                  def msbuild = tool name: 'MSBuild.exe', type: 'hudson.plugins.msbuild.MsBuildInstallation'
                  bat "\"C:\\Windows\\Microsoft.NET\\Framework64\\v4.0.30319\\${msbuild}\" ${WORKSPACE}\\SampleJenkinsPipeline\\SampleJenkins\\SampleApp.sln"
                } 
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
