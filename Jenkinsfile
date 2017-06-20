#!/usr/bin/env groovy
node {
	stage('Clean and Compile'){
		checkout scm
		dir('inventory'){
			//maven "versions:set -DnewVersion=2.0-SNAPSHOT"
			//maven "clean compile"
		}
		
	}
	stage('Test'){
		dir('inventory'){
			//maven "test"
		}
	}
	stage('Install'){
		dir('inventory'){
			//maven "install"
			tokens = sh (script: 'printf \'VERSION=${project.version}\\n0\\n\' | mvn org.apache.maven.plugins:maven-help-plugin:2.1.1:evaluate | grep \'^VERSION\'', returnStdout: true).split('=')
			echo "Project Version: ${tokens[1]}"
		}
	}

}
def maven(args){
	sh "mvn ${args}"
}

