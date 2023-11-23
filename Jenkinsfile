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
                sh "chmod +x /var/jenkins_home/workspace/itss-fe-pl/jenkins/scripts/test.sh"
                sh "chmod +x /var/jenkins_home/workspace/itss-fe-pl/jenkins/scripts/deliver.sh"
                sh "chmod +x /var/jenkins_home/workspace/itss-fe-pl/jenkins/scripts/kill.sh"
            }
        }
        stage("Print WorkingDirectory") {
            steps {
                sh 'pwd'
                sh 'ls -la'
                sh 'ls -la /var/jenkins_home/workspace/itss-fe-pl/jenkins'
                sh 'ls -la /var/jenkins_home/workspace/itss-fe-pl/jenkins/scripts'
            }
        }
        stage('Test') {
            steps {
                sh "/var/jenkins_home/workspace/itss-fe-pl/jenkins/scripts/test.sh"
            }
        }
        stage('Deliver') {
            steps {
                sh "/var/jenkins_home/workspace/itss-fe-pl/jenkins/scripts/deliver.sh"
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh "/var/jenkins_home/workspace/itss-fe-pl/jenkins/scripts/kill.sh"
            }
        }
    }
}
