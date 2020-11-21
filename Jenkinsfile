#!/usr/bin/env groovy
node {
//Hello Shilpi in IT
	String projectVersion = null
	String rpmName = null
	stage('Build'){
		checkout scm
		dir('inventory'){
			//projectVersion = createAndGetNewProjectVersion()
			//maven "versions:set -DnewVersion=${projectVersion}"
			//maven "clean install"
			//rpmName = 'wd-tomcat8-app-ilm-' + projectVersion + '-1.noarch.rpm'
			echo "building"
		}
		
	}
	stage('Test'){
		dir('inventory'){
			//maven "test"
			echo "testing"
		}
	}
	stage('Publish Artifacts'){
		def userInput = input (message: 'Want to deploy on QE now or schedule', parameters: [string(defaultValue: 'now', description: '', name: 'Time', trim: false)], submitterParameter: 'approver')

		dir('inventory'){
			//${rpmName}
			echo "Publishing artifacts for ${userInput.name}"			
		}
	}

}
def maven(args){
	sh "mvn ${args}"
}

def createAndGetNewProjectVersion(){
	//Fetching current pom version
	tokens = sh (script: 'printf \'VERSION=${project.version}\\n0\\n\' | mvn org.apache.maven.plugins:maven-help-plugin:2.1.1:evaluate | grep \'^VERSION\'', returnStdout: true).split('=')
	String currentVersion = tokens[1].replaceAll('\\n','').replaceAll('-SNAPSHOT','')
	//Fetching git commit Id
	String commitId = sh (script: 'git rev-parse --short=12 HEAD', returnStdout: true).trim()
	Date now = new Date()
	String strDateTime = now.format("YYYYMMDDHHmmss")
	return currentVersion + "_" + commitId + "_" + strDateTime
}

