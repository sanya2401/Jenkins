pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                // Cloning the repository from GitHub
                git 'https://github.com/sanya2401/Jenkins'  // Replace with your actual repository URL
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                // Use your own build script or direct commands for building the project
                bat 'build.bat'  // Replace with your actual build commands or scripts
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Run your test scripts or commands here
                bat 'run-tests.bat'  // Replace with your actual test commands
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code Quality...'
                // Example: Running a code analysis tool like ESLint, or any other tool you're using
                bat 'npm run lint'  // Example for a Node.js project; replace with your analysis tool or script
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Example: Running OWASP Dependency-Check or another security tool
                bat 'dependency-check.bat --project JenkinsPipeline --scan ./'  // Replace with your security scan tool or script
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging Server...'
                // Use a deployment script or file transfer command (replace with your actual deployment process)
                bat 'pscp.exe target\\my-app.jar user@staging-server:/deployments/'  // Example for SCP; replace with your actual deployment command
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Run tests on the staging environment (modify based on your actual test script)
                bat 'curl.exe -s http://staging-server:8080/api/test | findstr "All tests passed"'  // Example for an HTTP test; replace with your actual test command
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Server...'
                // Use a deployment script or file transfer command (replace with your actual deployment process)
                bat 'pscp.exe target\\my-app.jar user@production-server:/deployments/'  // Example for SCP; replace with your actual deployment command
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
            // Any cleanup tasks can go here
        }
    }
}
