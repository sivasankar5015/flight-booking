pipeline {
	agent any

	stages {
		stage("Maven-Build"){
			steps {
				sh 'mvn clean package'
			}
		}
		stage ("Docker-Login") {
			steps {
				sh 'docker login -u siva3100 -p Siva@5015'
			}
		}
		stage ("Deleting-Previous-Docker-Builds"){
			steps {
				sh 'docker rmi -f "$(docker images -aq)"'
			}
		}
		stage ("Docker-Build-Services") {
			steps {
				sh "docker build -t search:0.${env.BUILD_ID} search/"
				sh "docker build -t website:0.${env.BUILD_ID} website/"
			}
		}
		stage ("Tagging-docker-images") {
			steps {
				sh "docker tag search:0.${env.BUILD_ID} siva3100/search:0.${env.BUILD_ID}"
				sh "docker tag website:0.${env.BUILD_ID} siva3100/website:0.${env.BUILD_ID}"
			}
		}
		stage ("Pushing-Images-to-Registry"){
			steps {
				sh "docker push siva3100/search:0.${env.BUILD_ID}"
				sh "docker push siva3100/website:0.${env.BUILD_ID}"
			}
		}
		stage('DeployToProduction') {
            		steps {
                		kubernetesDeploy(
                    			kubeconfigId: 'kubeconfig',
                    			configs: 'flight-booking-kube.yml'
                		)
            		}
        	}
	}
}
