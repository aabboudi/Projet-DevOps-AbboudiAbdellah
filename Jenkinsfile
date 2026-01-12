pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Running Python Application...'
                sh 'python3 main.py'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'main.py', fingerprint: true
            }
        }

        stage('Notify Slack') {
            steps {
                slackSend channel: '#FPL-DEVOPS', 
                          message: "SUCCESS: Pipeline-Abdellah-Abboudi has completed successfully!"
            }
        }
    }
    
    post {
        failure {
            slackSend channel: '#FPL-DEVOPS', 
                      color: 'danger',
                      message: "FAILED: Pipeline-Abdellah-Abboudi has failed."
        }
    }
}