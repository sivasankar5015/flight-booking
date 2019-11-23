pipeline {
	agent any
	tools {
		jdk 'localJDK'
		maven 'localMaven'
	}
	stages {
		stage("Maven-Build"){
			steps {
				sh 'mvn -Dmaven.test.skip=true install'
			}
		}
		stage("Docker-Build"){
			steps {
				sh "docker build -t search:${env.BUILD_ID} search/"
			}
		}
	}
}
