pipeline{
	agent any
	environment {
		DOCKERHUB_PASS = 'Sridevi@2000'
	}
	stages{
		stage("Building the Student Survey Image"){
			steps{
				script{
					checkout scm
					sh 'rm -rf *.war'
					sh 'jar -cvf Student.war -C src/main/webapp .'
					sh 'docker login -u smovva2 -p ${DOCKERHUB_PASS}'
					sh 'docker build -t smovva2/student-survey .'
				}
			}
		}
		stage("Pushing image to docker"){
			steps{
				script{
					sh 'docker push smovva2/student-survey'
				}
			}
		}
		stage("Deploying to rancher"){
			steps{
				script{
				
					sh 'kubectl rollout restart deploy devip -n surveyform'
				}
			}
		}
	}
}