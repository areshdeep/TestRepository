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
                  bat "\"${msbuild}\" ${WORKSPACE}\\SampleJenkinsPipeline\\SampleJenkins\\SampleApp.sln /t:clean /t:build /p:Configuration=Release /p:DeployOnBuild=true /p:WebPublishMethod=Package  /p:PackageAsSingleFile=true /p:SkipInvalidConfigurations=true /p:DesktopBuildPackageLocation=${WORKSPACE}\\output.zip"
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
