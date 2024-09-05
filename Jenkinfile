pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example using Maven to build the project
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Example using Maven for running tests
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code Quality...'
                // Example using SonarQube scanner
                sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Example using OWASP Dependency-Check
                sh 'dependency-check.sh --project JenkinsPipeline --scan ./'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging Server...'
                // Example deployment command, replace with actual deployment script
                sh 'scp target/my-app.jar user@staging-server:/deployments/'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Example of integration tests on staging
                sh 'curl -s http://staging-server:8080/api/test | grep "All tests passed"'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Server...'
                // Example deployment command to production
                sh 'scp target/my-app.jar user@production-server:/deployments/'
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
