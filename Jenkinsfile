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
				sh 'docker run --rm -vjenkins:/var/jenkins_home -v/var/run/docker.sock:/var/run/docker.sock -vm2:/root/.m2 -w"$PWD" --net=ci_default maven:3.5.2-jdk-8-alpine mvn --settings settings.xml deploy'
				sh 'docker push nexus:8082/com.example/helloworld'
			}
		}
	}
}
