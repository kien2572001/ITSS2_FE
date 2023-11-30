pipeline {
    agent {
        docker {
            image 'node:20.10.0-alpine3.18'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Clean') {
            steps {
                script {
                    // Xóa thư mục node_modules
                    sh 'rm -rf node_modules'
                }
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
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