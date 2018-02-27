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
                  def msbuild = tool name: 'MsBuild', type: 'hudson.plugins.msbuild.MsBuildInstallation'
                  bat "\"${msbuild}\\msbuild.exe\" ${WORKSPACE}\\SampleJenkins\\SampleApp.sln"
                } 
            }
        }
	    stage('Testing') {
			steps {
				echo 'Testing..'
				script {
					def msbuild = tool name: 'MSBuild', type: 'hudson.plugins.msbuild.MsBuildInstallation'
					bat "\"${msbuild}\\msbuild.exe\" ${WORKSPACE}\\SampleJenkins\\SampleAppTest\\SampleAppTest.csproj"
                }
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
