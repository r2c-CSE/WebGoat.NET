@Library('semgrep') _

pipeline {
  agent any
    environment {
      // The following variable is required for a Semgrep Cloud Platform-connected scan:
      SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
      SEMGREP_BASELINE_REF = "origin/master"
      SEMGREP_BRANCH = "TEST6"
      SEMGREP_COMMIT = "${GIT_COMMIT}"
      SEMGREP_REPO_NAME = env.GIT_URL.replaceFirst(/^https:\/\/github.com\/(.*)$/, '$1')
      SEMGREP_REPO_URL = env.GIT_URL.replaceFirst(/^(.*).git$/,'$1')
      SEMGREP_PR_ID = "${env.CHANGE_ID}"
    }
    stages {
      stage('Print-Vars') {
        steps {
          sh 'printenv'
        }
      }
      /*stage('Semgrep-Full-Scan') {
        steps {
                script {
                    if (env.GIT_BRANCH == 'origin/master') {
                        echo 'Hello from master branch'
                        semgrepFullScan()
                    }  else {
                        sh "echo 'Hello from ${env.GIT_BRANCH} branch!'"
                    }
                }
            }
        }*/
        stage("Semgrep-Dbox-scan") {
            steps {
                    script {
                        sh "git --version"
                        sh "echo ${SEMGREP_PR_ID}"
                        sh "git checkout ${SEMGREP_BASELINE_REF}"
                        sh "git rev-parse HEAD"
                        sh "git checkout ${SEMGREP_BRANCH}"
                        // Debug here by checking if all env vars are set - sh 'printenv | grep SEMGREP'
                        // This is so that we fail-open except when exit status code is 1 for finding based result
                        //sh '$HOME/.local/bin/semgrep ci --baseline-commit=$(git merge-base trunk HEAD) || [ $? != 1 ]'
                        semgrepFullScanWithAllEnvVars()
                    }
            }
        }
    }
}
