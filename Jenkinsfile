pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                // Replace 'your-credentials-id' with the actual credentials ID you've set in Jenkins
                // Replace 'main' with the branch you are using (if it's not 'main')
                git branch: 'main', url: 'https://github.com/sanya2401/Jenkins', credentialsId: 'your-credentials-id'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Use your build script or commands here (replace with actual build commands)
                bat 'build.bat'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Add your test commands here (replace with actual test commands)
                bat 'run-tests.bat'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code Quality...'
                // Add your code analysis tool commands here (replace with actual commands)
                bat 'npm run lint'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Add your security scan commands here (replace with actual security scan commands)
                bat 'dependency-check.bat --project JenkinsPipeline --scan ./'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging Server...'
                // Use your deployment script or commands here
                bat 'pscp.exe target\\my-app.jar user@staging-server:/deployments/'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Replace with actual integration test commands
                bat 'curl.exe -s http://staging-server:8080/api/test | findstr "All tests passed"'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Server...'
                // Use your production deployment script or commands here
                bat 'pscp.exe target\\my-app.jar user@production-server:/deployments/'
            }
        }
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
            // Any cleanup tasks if necessary
        }
    }
}
