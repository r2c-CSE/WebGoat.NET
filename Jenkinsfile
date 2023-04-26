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
          //steps {
            if (env.GIT_BRANCH == 'origin/master') {
              echo 'Push!'
              semgrepFullScan()
            }
            else {
              echo 'Pull Request!'
            }
        //}
      }
    }
}
