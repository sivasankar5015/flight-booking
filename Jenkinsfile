pipeline {
	agent any
	tools {
		jdk 'localJDK'
		maven 'localMaven'
	}
	stages {
		stage("Build"){
			steps {
				sh 'mvn -Dmaven.test.skip=true install'
			}
		}
	}
}
