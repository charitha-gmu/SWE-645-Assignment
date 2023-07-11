pipeline{
	agent any
	environment {
		DOCKERHUB_PASS = 'Cherrym_1998'
	}
	stages{
		stage("Generating the Build for SWE645 student survey"){
			steps{
				script{
					checkout scm
					sh 'rm -rf *.war'
					sh 'jar -cvf SWE645Assignment2.war -C src/main/webapp .'
					sh 'docker login -u smeka2 -p ${DOCKERHUB_PASS}'
					sh 'docker build -t smeka2/swe-645-assignment-2-docker-image .'
				}
			}
		}
		stage("Pushing image to docker"){
			steps{
				script{
					sh 'docker push smeka2/'
				}
			}
		}
		stage("Deploying to rancher"){
			steps{
				script{
				
					sh 'kubectl rollout restart deploy deployment1 -n assignments'
				}
			}
		}
	}
}