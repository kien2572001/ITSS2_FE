pipeline {
    agent {
        docker {
            image 'node:20.10.0-alpine3.18'
            args '-p 3000:3000 -d --name itss2-fe'
        }
    }
    environment {
        HOME = '.'
    }
    stages {
        stage('Clean') {
            steps {
                script {
                    // Xóa Docker container cũ (nếu tồn tại)
                    sh 'docker rm -f itss2-fe || true'
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
        stage('Add Permission') {
            steps {
                sh 'chmod +x ./jenkins/scripts/*.sh'
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
                echo 'Deployed successfully!'
                // input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                // sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}