pipeline {
	agent any
	triggers { pollSCM('*/1 * * * *') }
	
	stages {
		stage('checkout') {
			steps {
				checkout scm
			}
		}
		stage('build & publish') {
			steps {
				sh 'docker run --rm -v"$PWD":/usr/src/workspace -w/usr/src/workspace maven:3.5.2-jdk-8-alpine mvn --settings settings.xml compile'
			}
		}
	}
}