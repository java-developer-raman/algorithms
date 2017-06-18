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
		}
	}

}
def maven(args){
	sh "mvn ${args}"
}

