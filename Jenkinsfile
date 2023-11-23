pipeline {
    agent {
        docker {
            image 'node:20.9.0-alpine3.18' 
            args '-p 3000:3000'
        }
    }
    environment {
        SCRIPTS_PATH = "$WORKSPACE/jenkins/scripts"
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
        stage('Set Permissions') {
            steps {
                sh "chmod +x ${SCRIPTS_PATH}/test.sh"
                sh "chmod +x ${SCRIPTS_PATH}/deliver.sh"
                sh "chmod +x ${SCRIPTS_PATH}/kill.sh"
            }
        }
        stage("Print WorkingDirectory") {
            steps {
                sh 'pwd'
                sh 'ls -la'
                sh 'ls -la ./jenkins'
                sh 'ls -la ./jenkins/scripts'
            }
        }
        stage('Test') {
            steps {
                sh "${SCRIPTS_PATH}/test.sh"
            }
        }
        stage('Deliver') {
            steps {
                sh "${SCRIPTS_PATH}/deliver.sh"
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh "${SCRIPTS_PATH}/kill.sh"
            }
        }
    }
}