pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Do not use 'sudo' within Docker containers
                    sh 'sudo node -v'
                    sh 'sudo npm install'
                }
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