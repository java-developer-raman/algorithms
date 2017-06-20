#!/usr/bin/env groovy
node {
	String hello = 'Build'
	stage('Build'){
		checkout scm
		dir('inventory'){
			echo "Haan ji ${hello}"
			hello = 'Test'
			//String newProjectVersion = createAndGetNewProjectVersion(getCurrentProjectVersion())
			//maven "versions:set -DnewVersion=${newProjectVersion}"
			//maven "clean compile"
		}
		
	}
	stage('Test'){
		dir('inventory'){
			//maven "test"
			echo "Haan ji ${hello}"
		}
	}
	stage('Publish Artifacts'){
		dir('inventory'){
			
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
String createAndGetNewProjectVersion(String projectVersion){
	commitId = sh (script: 'git rev-parse --short=12 HEAD', returnStdout: true).trim()
	Date now = new Date()
	String strDateTime = now.format("YYYYMMDDHHmmss")
	return commitId + "_" + strDateTime
}

