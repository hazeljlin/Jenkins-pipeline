pipeline {
  agent any
  environment {
    EMAIL_RECIPIENT = "jxl1712@gmail.com"
  }
  stages {
    stage('Build') {
      steps {
        echo "Stage 1: Building the code using Maven and GitLab CI/CD"
      }
    }
    stage('Unit and Integration Tests') {
      steps {
        echo "Stage 2: Running unit tests and integration tests using Jest"
      }
      post {
        success {
          emailext(
            to: "${EMAIL_RECIPIENT}",
            subject: "Unit and Integration Tests Passed",
            body: "The Unit and Integration Tests stage was successful.",
            attachLog: true
          )
        }
        failure {
          emailext(
            to: "${EMAIL_RECIPIENT}",
            subject: "Unit and Integration Tests Failed",
            body: "The Unit and Integration Tests stage failed. Please check the attached logs for details.",
            attachLog: true
          )
        }
      }
    }
    stage('Code Analysis') {
      steps {
        echo "Stage 3: Integrate a code analysis tool to analyze the code using Jenkins"
      }
    }
    stage('Security Scan') {
      steps {
        echo "Stage 4: Performing a security scan using Burp Suite"
      }
      post {
        success {
          emailext(
            to: "${EMAIL_RECIPIENT}",
            subject: "Security Scan Passed",
            body: "The Security Scan stage was successful.",
            attachLog: true
          )
        }
        failure {
          emailext(
            to: "${EMAIL_RECIPIENT}",
            subject: "Security Scan Failed",
            body: "The Security Scan stage failed. Please check the attached logs for details.",
            attachLog: true
          )
        }
      }
    }
    stage('Deploy to Staging') {
      steps {
        echo "Stage 5: Deploying the application to the staging server using AWS"
      }
    }
    stage('Integration Tests on Staging') {
      steps {
        echo "Stage 6: Running integration tests on the staging environment"
      }
    }
    stage('Deploy to Production') {
      steps {
        echo "Stage 7: Deploying the application to the production server using AWS"
      }
    }
  }
  post {
    success {
      echo "Pipeline completed successfully!"
    }
    failure {
      echo "Pipeline failed."
    }
  }
}



