pipeline {
    agent any

    tools {
     maven 'Maven 3.x'
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                sh 'mvn clean install'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'mvn test'
            }
            post {
                always {
                    echo 'Sending email notification for Unit and Integration Tests...'
                    script {
                        def log = currentBuild.rawBuild.getLog(100).join("\n")
                        mail to: 's223083133@deakin.edu.au',
                             subject: "Unit and Integration Tests: ${currentBuild.currentResult}",
                             body: "The status of the Unit and Integration Tests stage is ${currentBuild.currentResult}. Please see the attached log.",
                             attachments: [[fileName: "unit_integration_tests_log.txt", content: log]]
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'mvn org.owasp:dependency-check-maven:check'
            }
            post {
                always {
                    echo 'Sending email notification for Security Scan...'
                    script {
                        def log = currentBuild.rawBuild.getLog(100).join("\n")
                        mail to: 's223083133@deakin.edu.au',
                             subject: "Security Scan: ${currentBuild.currentResult}",
                             body: "The status of the Security Scan stage is ${currentBuild.currentResult}. Please see the attached log.",
                             attachments: [[fileName: "security_scan_log.txt", content: log]]
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                sh 'scp target/your-app.jar jxl@192.168.0.101:/Users/jxl/Desktop/Jenkins_pipeline'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'ssh jxl@192.168.0.101 "cd /Users/jxl/Desktop/Jenkins_pipeline && ./run-tests.sh"'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                sh 'scp target/your-app.jar jxl@192.168.0.101:/Users/jxl/Desktop/Jenkins_pipeline'
            }
        }
    }
}

