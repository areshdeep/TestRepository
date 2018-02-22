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
                  bat "\"${msbuild}\" ${WORKSPACE}\\SampleJenkinsPipeline\\SampleJenkins\\SampleApp.sln"
                } 
            }
        }
	    stage('Testing') {
			steps {
				echo 'Testing..'
				script {
					def msbuild = tool name: 'MSBuild.exe', type: 'hudson.plugins.msbuild.MsBuildInstallation'
					bat "\"${msbuild}\" ${WORKSPACE}\\mstest.proj "
                }
	        step([$class: 'MSTestPublisher', testResultsFile:"**/*.trx", failOnError: true, keepLongStdio: true])
			 publishHTML target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'TestResults',
            reportFiles: 'summary.htm',
            reportName: 'CoverageReport'
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
				def sqScannerMsBuildHome = tool name:'Morgan-SONAR', type: 'hudson.plugins.sonar.MsBuildSQRunnerInstallation'
				def msbuild = tool name: 'MSBuild.exe', type: 'hudson.plugins.msbuild.MsBuildInstallation'
				
				withSonarQubeEnv('DOJO-SONAR') {
				  
				  bat "${sqScannerMsBuildHome}\\SonarQube.Scanner.MSBuild.exe begin /k:MOR-rule-service /n:TestRepository /v:$BUILD_NUMBER /d:sonar.host.url=https://tools.publicis.sapient.com/sonar /d:sonar.login=689af1124db29b5683bca49f44dd8d74ddc803fe /d:sonar.cs.vstest.reportsPaths=\"TestResults\\*.trx\" /d:sonar.cs.opencover.reportsPaths=\"Latest\\coverage-log.xml\""
				  bat "\"${msbuild}\" ${WORKSPACE}\\SampleJenkinsPipeline\\SampleJenkins\\SampleApp.sln /t:clean /t:build /p:Configuration=Release"
				  bat "\"${msbuild}\" ${WORKSPACE}\\SampleJenkins\\SampleAppTest\\SampleAppTest.proj"
				  bat "${sqScannerMsBuildHome}\\SonarQube.Scanner.MSBuild.exe end"
				}
					
			}
		}
	}
}
