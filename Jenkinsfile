#!/usr/bin/env groovy
node {
	stage('Clean and Compile'){
		checkout scm
		dir('inventory'){
			maven "versions:set -DnewVersion=2.0-SNAPSHOT"
			maven "clean compile"
		}
		
	}
	stage('Test'){
		dir('inventory'){
			maven "test"
		}
	}
	stage('Install'){
		dir('inventory'){
			maven "install"
			GIT_COMMIT_EMAIL = sh (script: 'mvn org.apache.maven.plugins:maven-help-plugin:2.1.1:evaluate -Dexpression=project.version', returnStdout: true).trim()
			echo "Git committer email: ${GIT_COMMIT_EMAIL}"
		}
	}

}
def maven(args){
	sh "mvn ${args}"
}

