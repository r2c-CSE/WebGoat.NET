@Library('semgrep') _

pipeline {
  agent any
    environment {
      // The following variable is required for a Semgrep Cloud Platform-connected scan:
      SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
    }
    stages {
      stage('Print-Vars') {
        steps {
          echo "The build number is ${env.BUILD_NUMBER}"
          echo "The git branch is ${env.GIT_BRANCH}"
          echo "The branch name is ${env.BRANCH_NAME}"
          sh 'printenv'
        }
      }
      stage('Semgrep-Scan') {
        steps {
                script {
                    if (env.BRANCH_NAME == 'origin/master') {
                        echo 'Hello from main branch'
                        semgrepFullScan()
                    }  else {
                        sh "echo 'Hello from ${env.BRANCH_NAME} branch!'"
                    }
                }
            }
        }
    }
}
