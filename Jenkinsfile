pipeline {
    agent any
    
    environment {
        MAVEN_HOME = tool 'Maven'
        SONAR_SCANNER_HOME = tool 'SonarQube Scanner' // SonarQube scanner
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh "${MAVEN_HOME}/bin/mvn clean package"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                sh "${MAVEN_HOME}/bin/mvn test"
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running SonarQube Code Analysis...'
                withSonarQubeEnv('SonarQube') { // SonarQube environment
                    sh "${SONAR_SCANNER_HOME}/bin/sonar-scanner"
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                sh 'dependency-check --project my-app --out reports --scan ./'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                sh 'ansible-playbook -i staging_inventory deploy.yml'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                sh 'postman run my-integration-tests.postman_collection.json'

            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                sh 'terraform apply -auto-approve'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
