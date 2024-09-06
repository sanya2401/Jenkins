pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Use Maven command for Windows (assuming Maven is installed and configured in PATH)
                bat 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Running tests with Maven on Windows
                bat 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code Quality...'
                // Running SonarQube scanner on Windows, make sure SonarQube is installed and configured
                bat 'sonar-scanner.bat'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Running OWASP Dependency-Check on Windows (assuming it's installed)
                bat 'dependency-check.bat --project JenkinsPipeline --scan ./'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging Server...'
                // Use a deployment script that works for Windows
                // For example, use WinSCP or PowerShell script for SCP-like behavior
                // bat 'pscp.exe target\\my-app.jar user@staging-server:/deployments/'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Running curl for Windows (ensure curl is installed or use Invoke-WebRequest with PowerShell)
                bat 'curl.exe -s http://staging-server:8080/api/test | findstr "All tests passed"'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Server...'
                // Use a deployment script that works for Windows (e.g., WinSCP, PowerShell)
                // bat 'pscp.exe target\\my-app.jar user@production-server:/deployments/'
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
