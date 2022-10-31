pipeline {
    agent {
        docker {
            image 'node:lts-bullseye-slim' 
            args '-p 3000:3000' 
        }
    }
    stages {
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
            stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan eksekusi pipeline ke tahap Deploy)'
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                sleep(time:1, unit:"MINUTES")
                
            }
        }
    }
}