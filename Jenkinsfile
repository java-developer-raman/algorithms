#!/usr/bin/env groovy
node {
	stage('Build'){
		echo "Checking out source code";
		checkout scm
		dir('inventory'){
			maven "clean install"
		}
		
	}
}
def maven(args){
	sh "mvn ${args}"
}

