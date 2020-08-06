pipeline {
    agent {
        docker { image 'node:7-alpine' }
    }
	environment {
		dockerHome = tool 'myDocker'
		MavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$MavenHome/bin:$PATH"
	}
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}