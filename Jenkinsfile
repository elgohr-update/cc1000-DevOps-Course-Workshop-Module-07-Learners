pipeline {
    agent none

    stages {
        stage('Install web dependencies') {
			agent {
				docker { image 'node:14-alpine' }
			}
            steps {
				dir("DotnetTemplate.Web") {
					// Needed as get SSL failure otherwise. May be due to wrong system date/time in container.
					sh 'npm config set strict-ssl false && npm config set unsafe-perm true && npm config set registry http://registry.npmjs.org/'
					
					sh 'npm install'
				}
            }
        }
		
        stage('Web build') {
			agent {
				docker { image 'node:14-alpine' }
			}
            steps {
				dir("DotnetTemplate.Web") {					
					sh 'npm run build'
				}
            }
        }
		
        stage('TypeScript linting') {
			agent {
				docker { image 'node:14-alpine' }
			}
            steps {
				dir("DotnetTemplate.Web") {					
					sh 'npm run lint'
				}
            }
        }
		
        stage('Web tests') {
			agent {
				docker { image 'node:14-alpine' }
			}
            steps {
				dir("DotnetTemplate.Web") {					
					sh 'npm t'
				}
            }
        }
    }
}