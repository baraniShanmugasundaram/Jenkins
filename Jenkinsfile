pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Tool: Maven
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests...'
                // Tool: JUnit
                echo 'Running integration tests...'
                // Tool: Selenium
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Running code analysis...'
                // Tool: SonarQube
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Tool: OWASP ZAP
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
                // Tool: AWS CLI
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Tool: Postman
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                // Tool: AWS CLI
            }
        } 
    }
    
    post {
        success {
            emailext subject: "Build Status Email - Success",
                body: "Build was successful!",
                to: "barani6778@gmail.com",
                attachmentsPattern: '*.log' // Attach all log files
        }
        failure {
            emailext subject: "Build Status Email - Failure",
                body: "Build failed!",
                to: "barani6778@gmail.com",
                attachmentsPattern: '*.log' // Attach all log files
        }
    }
}
