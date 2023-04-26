@Library('semgrep') _

pipeline {
  agent any
    environment {
      // The following variable is required for a Semgrep Cloud Platform-connected scan:
      SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')

    }
    stages {
      stage('Semgrep-Scan-Full-Scan') {
        when {
          branch 'origin/master'
        }
        steps {
          echo 'Push!'
          semgrepFullScan()
       }
    }
    stages {
      stage('Semgrep-Scan-Pull-Request-Scan') {
        when {
          changeRequest target: 'origin/master'
        }
        steps {
          echo 'Pull Request!'
       }
    }
  }
}
