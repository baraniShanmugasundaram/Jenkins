pipeline {
    agent any

    environment {
        CODE_DIRECTORY = "/path/to/code"
        TEST_ENV = "testing"
        PROD_ENV = "yourname_production"
        NOTIFICATION_EMAIL = "barani6778@gmail.com"
        LOG_PATH = "${WORKSPACE}\\logs"  // Use Jenkins workspace for logs
    }

    stages {
        stage('Build') {
            steps {
                script {
                    bat "mkdir \"${env.LOG_PATH}\""
                    bat "echo Fetching the source code from: $CODE_DIRECTORY > \"${env.LOG_PATH}\\build.log\""
                    bat "echo Compiling the code and generating artifacts >> \"${env.LOG_PATH}\\build.log\""
                    // Replace /path/to/code with actual path or build commands
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    bat "echo Running unit tests > \"${env.LOG_PATH}\\unit_tests.log\""
                    bat "echo Running integration tests >> \"${env.LOG_PATH}\\unit_tests.log\""
                    // Add actual test execution commands and output to unit_tests.log
                }
            }
            post {
                success {
                    emailext (
                        subject: "Unit and Integration Tests Passed",
                        body: "Unit and Integration Tests have passed successfully. See attached logs for details.",
                        to: "${env.NOTIFICATION_EMAIL}",
                        mimeType: 'text/html',
                        attachmentsPattern: "\"${env.LOG_PATH}\\unit_tests.log\""
                    )
                }
                failure {
                    emailext (
                        subject: "Unit and Integration Tests Failed",
                        body: "Unit and Integration Tests have failed. See attached logs for details.",
                        to: "${env.NOTIFICATION_EMAIL}",
                        mimeType: 'text/html',
                        attachmentsPattern: "\"${env.LOG_PATH}\\unit_tests.log\""
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    bat "echo Checking the quality of the code > \"${env.LOG_PATH}\\code_analysis.log\""
                    // Add code quality check commands and output to code_analysis.log
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    bat "echo Performing security scan > \"${env.LOG_PATH}\\security_scan.log\""
                    // Add security scan commands and output to security_scan.log
                }
            }
            post {
                success {
                    emailext (
                        subject: "Security Scan Passed",
                        body: "Security scan completed without any vulnerabilities. See attached logs for details.",
                        to: "${env.NOTIFICATION_EMAIL}",
                        mimeType: 'text/html',
                        attachmentsPattern: "\"${env.LOG_PATH}\\security_scan.log\""
                    )
                }
                failure {
                    emailext (
                        subject: "Security Scan Failed",
                        body: "Security scan detected vulnerabilities. See attached logs for details.",
                        to: "${env.NOTIFICATION_EMAIL}",
                        mimeType: 'text/html',
                        attachmentsPattern: "\"${env.LOG_PATH}\\security_scan.log\""
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    bat "echo Deploying the application to the $TEST_ENV environment > \"${env.LOG_PATH}\\staging_deploy.log\""
                    // Add deployment commands to staging and output to staging_deploy.log
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    bat "echo Running integration tests on staging environment > \"${env.LOG_PATH}\\staging_tests.log\""
                    // Add integration tests on staging commands and output to staging_tests.log
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    bat "echo Deploying the code to the $PROD_ENV environment > \"${env.LOG_PATH}\\production_deploy.log\""
                    // Add production deployment commands and output to production_deploy.log
                }
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Pipeline Status: ${currentBuild.result}",
                body: '''<html>
                    <body>
                    <p>Build Status: ${currentBuild.result}</p>
                    <p>Build Number: ${currentBuild.number}</p>
                    <p>See attached logs for details.</p>
                    </body>
                    </html>''',
                to: "${env.NOTIFICATION_EMAIL}",
                from: 'jenkins@example.com',
                replyTo: 'jenkins@example.com',
                mimeType: 'text/html',
                attachmentsPattern: "\"${env.LOG_PATH}\\*.log\""
            )
        }
    }
}
