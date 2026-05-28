pipeline {
    agent {
        node {
            label 'Robohshop'
        }
    }
    options {
        timeout(time: 5, unit: 'MINUTES')
    }
    environment {
        appVersion = ''   
        appName = 'catalogue'      
    }

    stages {
        stage ('Read the version') {
            steps {
                script {
                    // Read and parse package.json from the workspace root
                    def packageJson = readJSON file: 'package.json'
                    
                    // Access individual properties
                    
                    def appVersion = packageJson.version                    
                    echo "Building ${appName} - Version: ${appVersion}"
                    
                    
                }
            }
        }
        stage ('Install dependencies') {
            steps {
                sh """
                echo "Installing dependencies for ${appName}"

                npm install
                """
            }
        }
        stage ('Build docker image') {
            steps {
                sh """
                docker build -t ${appName}:${appVersion} .
                
                """
            }
        }
    }
}