Library <TestGrrovy>
node {
   def mvnHome
   stage('Preparation') { 
   echo 'Preparation...'
      git 'https://github.com/jglick/simple-maven-project-with-tests.git'
   }
   stage('CheckOut') {
   echo 'CheckOut...'
        git url: 'https://github.com/areshdeep/TestRepository'
   }
   stage('Build') {
        echo 'Build code...'
    	bat "D:\\Work\\PPL\\Own\\Jenkinsetup\\nuget.exe restore ${WORKSPACE}\\SampleJenkins\\SampleJenkins.sln"
    	build "SampleJenkins"
    }
	stage('Testing') {
			echo 'Testing..'
	}
	stage('Deploy') {
			echo 'Deploy..'
	} 
	
	stage('SonarQube analysis') {
			echo 'Sonar Qube analysis..'
	}
}