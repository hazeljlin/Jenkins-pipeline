pipeline {
    agent any

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

    post {
        always {
            echo 'Sending email notifications...'
            mail to: 's223083133@deakin.edu.au',
                 subject: "Jenkins Pipeline: ${currentBuild.fullDisplayName}",
                 body: "Build ${currentBuild.currentResult}: ${env.BUILD_URL}"
        }
    }
}

