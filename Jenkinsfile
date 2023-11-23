pipeline {
    agent {
        docker {
            image 'node:20.9.0-alpine3.18' 
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
        stage("Print WorkingDirectory") {
            steps {
                sh 'pwd'
                sh 'ls -la'
            }
        }
        stage('Set Permissions') {
            steps {
                sh 'chmod +x ./jenkins/scripts/test.sh'
                sh 'chmod +x ./jenkins/scripts/deliver.sh'
                sh 'chmod +x ./jenkins/scripts/kill.sh'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }     
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}