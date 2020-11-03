pipeline {
    agent none

    stages {
        stage('Install web dependencies') {
			agent {
				docker { image 'node:14-alpine' }
			}
            steps {
				dir("DotnetTemplate.Web") {
					sh 'npm install'
				}				
            }
        }
    }
}