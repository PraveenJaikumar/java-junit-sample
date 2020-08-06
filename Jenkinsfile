pipeline {
	environment {
		dockerHome = tool 'myDocker'
		MavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$MavenHome/bin:$PATH"
	}
    agent {
        docker { image 'node:7-alpine' }
    }
	
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}