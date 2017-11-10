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
				sh 'docker run --rm -vci_jenkins:/var/jenkins_home -v/var/run/docker.sock:/var/run/docker.sock -vm2:/root/.m2 -w"$PWD" --net=ci_default maven:3.5.2-jdk-8-alpine mvn --settings settings.xml deploy'
				sh 'docker push nexus:8082/treeptik/helloworld'
			}
		}
    stage('Deploy QA') {
      steps {
        sh 'docker stop ci_QA || true && docker rm -f ci_QA || true'
        sh 'docker run -d -p --name ci_QA 8080:8080 nexus:8082/treeptik/helloworld:latest'
      }
    }
	}
}
