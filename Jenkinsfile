pipeline {
    agent none

    stages {
        stage('Install web dependencies') {
			agent {
				docker { image 'node:14-alpine' }
			}
            steps {
				dir("DotnetTemplate.Web") {
					sh 'npm config set strict-ssl false && npm config set unsafe-perm true && npm config set registry http://registry.npmjs.org/'
					sh 'npm install'
				}
            }
        }
    }
}