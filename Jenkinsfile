pipeline {
    agent any

    environment {
        CODE_DIRECTORY = "E:/Jenkinsfile/Jenkinsfile.txt"
        TEST_ENV = "testing"
        NOTIFICATION_EMAIL = "barani6778@gmail.com"
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from: $CODE_DIRECTORY"
                echo "Compiling the code and generating artifacts"
                // Add actual build steps here
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests"
                echo "Running integration tests"
                // Add actual test steps here
            }
            post {
                success {
                    mail to: "${env.NOTIFICATION_EMAIL}",
                         subject: "Unit and Integration Tests Passed",
                         body: "Unit and Integration Tests have passed successfully. See attached logs for details."
                }
                failure {
                    mail to: "${env.NOTIFICATION_EMAIL}",
                         subject: "Unit and Integration Tests Failed",
                         body: "Unit and Integration Tests have failed. See attached logs for details."
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Checking the quality of the code'
                // Add actual code quality check steps here
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan'
                // Add actual security scan steps here
            }
            post {
                success {
                    mail to: "${env.NOTIFICATION_EMAIL}",
                         subject: "Security Scan Passed",
                         body: "Security scan completed without any vulnerabilities. See attached logs for details."
                }
                failure {
                    mail to: "${env.NOTIFICATION_EMAIL}",
                         subject: "Security Scan Failed",
                         body: "Security scan detected vulnerabilities. See attached logs for details."
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on staging environment"
                // Add actual integration tests on staging steps here
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying the code to the $PROD_ENV environment"
                // Add actual production deployment steps here
            }
        }
    }
}
