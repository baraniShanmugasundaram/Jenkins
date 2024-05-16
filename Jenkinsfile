pipeline {
    agent any

    environment {
        CODE_DIRECTORY = "/path/to/code"
        TEST_ENV = "testing"
        PROD_ENV = "yourname_production"
        NOTIFICATION_EMAIL = "barani6778@gmail.com"
        LOGS_PATH = "C:\\Users\\baran\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\6.1C_Jenkins_Git\\logs"
    } 

    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from: $CODE_DIRECTORY" 
                echo "Compiling the code and generating artifacts"
                script {
                    // Save the console output to a file
                    sh "echo Fetching the source code from: $CODE_DIRECTORY > $LOGS_PATH\\build_logs.txt"
                    sh "echo Compiling the code and generating artifacts >> $LOGS_PATH\\build_logs.txt"
                    // Add actual build commands here and append output to the log file
                    // sh "<your-build-command> >> $LOGS_PATH\\build_logs.txt 2>&1"
                }
            }
            post {
                always {
                    emailext (
                        to: "${env.NOTIFICATION_EMAIL}",
                        subject: "Build Process Notification",
                        body: "The build process has completed. Please see the attached logs for details.",
                        attachments: ["$LOGS_PATH\\build_logs.txt"],
                        mimeType: 'text/html'
                    )
                }
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
                    emailext (
                        to: "${env.NOTIFICATION_EMAIL}",
                        subject: "Unit and Integration Tests Passed",
                        body: "Unit and Integration Tests have passed successfully. See attached logs for details.\nConsole Output: ${env.BUILD_URL}console",
                        mimeType: 'text/html'
                    )
                }
                failure {
                    emailext (
                        to: "${env.NOTIFICATION_EMAIL}",
                        subject: "Unit and Integration Tests Failed",
                        body: "Unit and Integration Tests have failed. See attached logs for details.\nConsole Output: ${env.BUILD_URL}console",
                        mimeType: 'text/html'
                    )
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
                    emailext (
                        to: "${env.NOTIFICATION_EMAIL}",
                        subject: "Security Scan Passed",
                        body: "Security scan completed without any vulnerabilities. See attached logs for details.\nConsole Output: ${env.BUILD_URL}console",
                        mimeType: 'text/html'
                    )
                }
                failure {
                    emailext (
                        to: "${env.NOTIFICATION_EMAIL}",
                        subject: "Security Scan Failed",
                        body: "Security scan detected vulnerabilities. See attached logs for details.\nConsole Output: ${env.BUILD_URL}console",
                        mimeType: 'text/html'
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to the $TEST_ENV environment"
                // Add actual staging deployment steps here
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

    post {
        always {
            emailext (
                subject: "Pipeline Status: ${currentBuild.result}",
                body: '''<html>
                    <body>
                    <p>Build Status: ${currentBuild.result}</p>
                    <p>Build Number: ${currentBuild.number}</p>
                    <p>Console Output: <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a></p>
                    </body>
                    </html>''',
                to: 'barani6778@gmail.com',
                from: 'jenkins@example.com',
                replyTo: 'jenkins@example.com',
                mimeType: 'text/html'
            )
        }
    }
}
