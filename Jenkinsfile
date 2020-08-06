pipeline {
	agent any
	environment {
		// dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$mavenHome/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:$PATH"
	}
	stages {
		stage('Checkout Source') {
			steps {
				echo 'Check out the project'
				echo "$PATH"
				checkout scm  
			}
		}
		stage('Maven Building Artifacts') {
			steps {			
				sh "mvn clean package"
				sh 'ls -lrta'
				sh 'pwd'
			}
		}	
		stage('Junit Test Results') {
			steps {			
				archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
				junit '**/target/surefire-reports/TEST-*.xml'
			}
		}
		stage('Build Docker Image') {
			steps {
				script {
					dockerImage = docker.build("praveenjaikumar/testdock:${env.BUILD_TAG}")
				}		
			//	sh "docker build -t sample/my-app:1.0.0 ."
				
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry( '', 'praveen-docker' ) {
						dockerImage.push()
						dockerImage.push('latest')
					}
				}			
			//	sh "docker build -t sample/my-app:1.0.0 ."
				
			}
		}

	}
}
