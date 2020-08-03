pipeline {
	agent any
	tools {
        maven 'maven-3.6.3' 
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
			bat "mvn clean install"
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
			bat "docker build -t sample/my-app:1.0.0 ."
		}
   }

}
}
