pipeline {
	agent any
	tools {
        maven 'myMaven' 
        }
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

    stage('Maven Building Artifacts'){
        steps {			
			//sh "mvn clean package"
		}
	}	
    stage('Junit Test Results') {
		steps {			
			junit '**/target/surefire-reports/TEST-*.xml'
			archiveArtifacts 'target/*.jar'
		}
   }
    stage('Build Docker Image'){
     	steps {		
		sh "docker build -t sample/my-app:1.0.0 ."
	}
   }

}
}
