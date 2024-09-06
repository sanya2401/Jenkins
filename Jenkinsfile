pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                git branch: 'main', url: 'https://github.com/sanya2401/Jenkins', credentialsId: '2c7d77af-f349-4265-a65d-263ae91e0ee1'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Replace with your actual build command
                bat 'npm install'  // Example for Node.js
                bat 'npm run build'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                bat 'npm test'  // Example for Node.js
            }
        }

        // Other stages...
    }

    post {
        success {
            emailext (
                to: 'arorasanya.2401@gmail.com',
                subject: "Jenkins Pipeline Success: ${currentBuild.fullDisplayName}",
                body: "Good news! The pipeline ${currentBuild.fullDisplayName} completed successfully.",
                attachLog: true
            )
        }
        failure {
            emailext (
                to: 'arorasanya.2401@gmail.com',
                subject: "Jenkins Pipeline Failure: ${currentBuild.fullDisplayName}",
                body: "Attention! The pipeline ${currentBuild.fullDisplayName} has failed. Please check the attached log for details.",
                attachLog: true
            )
        }
        always {
            echo 'Cleaning up...'
        }
    }
}
