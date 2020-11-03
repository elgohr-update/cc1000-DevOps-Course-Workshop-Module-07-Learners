pipeline {
    agent none
	
	environment {
		DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
	}

    stages {			
        stage('C# build') {
			agent {
				docker { image 'mcr.microsoft.com/dotnet/core/sdk:3.1' }
			}
            steps {
				sh 'dotnet build'
            }
        }
		
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