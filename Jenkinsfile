#!/usr/bin/groovy
@Library('testlib')_
 
try {
    node {
        stage '\u2777 Clean Up'
        stage '\u2776 Checkout'
        
		stage ('\u2777 Checkout') {
			CheckOut('https://github.com/areshdeep/TestRepository')
		}
		stage ('\u2777 Build') {
			bat "\"D:\\Work\\PPL\\Own\\Jenkinsetup\\nuget.exe\" restore \"${WORKSPACE}\\SampleJenkins\\SampleApp.sln\""
			script {
              def msbuild = tool name: 'MsBuild', type: 'hudson.plugins.msbuild.MsBuildInstallation'
              bat "\"${msbuild}\\msbuild.exe\" ${WORKSPACE}\\SampleJenkins\\SampleApp.sln"
            } 
		}
        
        stage '\u2777 Tesing'
        
        stage '\u2777 Deploy'
        
        stage '\u2777 SonarQube Analysis'
    }
} 
catch (exc) {
    print exc
} 