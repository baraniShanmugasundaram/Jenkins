pipeline {
    agent any

    environment {
        CODE_DIRECTORY = "/path/to/code"  // Ensure this is correctly set
        TEST_ENV = "testing"
        PROD_ENV = "yourname_production"
        NOTIFICATION_EMAIL = "barani6778@gmail.com"
        LOG_PATH = "${WORKSPACE}\\logs"  // Logs in the workspace directory
    }

    stages {
        stage('Build') {
            steps {
                script {
                    bat "if not exist \"${env.LOG_PATH}\" mkdir \"${env.LOG_PATH}\""
                    bat "echo Fetching the source code from: $CODE_DIRECTORY > \"${env.LOG_PATH}\\build.log\""
                    bat "echo Compiling the code and generating artifacts >> \"${env.LOG_PATH}\\build.log\""
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    bat "if not exist \"${env.LOG_PATH}\" mkdir \"${env.LOG_PATH}\""
                    bat "echo Running unit tests > \"${env.LOG_PATH}\\unit_tests.log\""
                    bat "echo Running integration tests >> \"${env.LOG_PATH}\\unit_tests.log\""
                }
            }  
            post {
                success {
                    emailext (
                        subject: "Unit and Integration Tests Passed",
                        body: "All unit and integration tests have passed. See Jenkins for details.",
                        to: "${env.NOTIFICATION_EMAIL}"
                    )
                }
                failure {
                    emailext (
                        subject: "Unit and Integration Tests Failed",
                        body: "Some unit or integration tests have failed. Check Jenkins for more information.",
                        to: "${env.NOTIFICATION_EMAIL}"
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    bat "if not exist \"${env.LOG_PATH}\" mkdir \"${env.LOG_PATH}\""
                    bat "echo Performing code analysis > \"${env.LOG_PATH}\\code_analysis.log\""
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    bat "if not exist \"${env.LOG_PATH}\" mkdir \"${env.LOG_PATH}\""
                    bat "echo Performing security scan > \"${env.LOG_PATH}\\security_scan.log\""
                }
            }
            post {
                success {
                    emailext (
                        subject: "Security Scan Passed",
                        body: "Security scan completed successfully without any vulnerabilities.",
                        to: "${env.NOTIFICATION_EMAIL}"
                    )
                }
                failure {
                    emailext (
                        subject: "Security Scan Failed",
                        body: "Security scan detected vulnerabilities. Please review the scan results.",
                        to: "${env.NOTIFICATION_EMAIL}"
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    bat "if not exist \"${env.LOG_PATH}\" mkdir \"${env.LOG_PATH}\""
                    bat "echo Deploying to staging environment > \"${env.LOG_PATH}\\staging_deploy.log\""
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    bat "if not exist \"${env.LOG_PATH}\" mkdir \"${env.LOG_PATH}\""
                    bat "echo Running integration tests on staging > \"${env.LOG_PATH}\\staging_tests.log\""
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    bat "if not exist \"${env.LOG_PATH}\" mkdir \"${env.LOG_PATH}\""
                    bat "echo Deploying to production environment > \"${env.LOG_PATH}\\production_deploy.log\""
                }
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Pipeline Status: ${currentBuild.result}",
                body: "Pipeline execution complete with status: ${currentBuild.result}. Check Jenkins for more details.",
                to: "${env.NOTIFICATION_EMAIL}"
            )
        }
    }
}
