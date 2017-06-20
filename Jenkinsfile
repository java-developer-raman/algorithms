#!/usr/bin/env groovy
node {
	String projectVersion = null
	stage('Build'){
		checkout scm
		dir('inventory'){
			createNewProjectVersion()
			maven "versions:set -DnewVersion=${projectVersion}"
			maven "clean compile"
		}
		
	}
	stage('Test'){
		dir('inventory'){
			maven "test"
		}
	}
	stage('Publish Artifacts'){
		dir('inventory'){
			echo "Publishing artifacts for ${projectVersion}"			
		}
	}

}
def maven(args){
	sh "mvn ${args}"
}

String getCurrentProjectVersion(){
	tokens = sh (script: 'printf \'VERSION=${project.version}\\n0\\n\' | mvn org.apache.maven.plugins:maven-help-plugin:2.1.1:evaluate | grep \'^VERSION\'', returnStdout: true).split('=')
			echo "Project Version: ${tokens[1]}"
	return ${tokens[1]}
}
String createNewProjectVersion(String projectVersion){
	String currentVersion = getCurrentProjectVersion()
	String commitId = sh (script: 'git rev-parse --short=12 HEAD', returnStdout: true).trim()
	Date now = new Date()
	String strDateTime = now.format("YYYYMMDDHHmmss")
	return currentVersion + "_" + commitId + "_" + strDateTime
}

