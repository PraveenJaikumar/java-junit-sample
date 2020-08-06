pipeline {
	agent any
	environment {
		dockerHome = tool 'myDocker'
		MavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$MavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout Source') {
			steps {
				echo 'Check out the project'
				checkout scm  
			}
		}
		stage('Maven Building Artifacts') {
			steps {			
				sh "mvn clean package"
				echo 'Check out the project'
			}
		}	
		stage('Junit Test Results') {
			steps {			
				archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
				junit '**/target/surefire-reports/TEST-*.xml'
			}
		}
		stage('Build Docker Image'){
			steps {		
			sh "docker build -t sample/my-app:1.0.0 ."
			}
		}
	}
}
