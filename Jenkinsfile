pipeline {
  agent any
  environment {
    APPSYSID = '69d0c8b347112110fb6e7ac8f36d438d'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS = '4a37b613-0182-45c9-b0d7-d829bd88d3f6'
    DEVENV = 'https://dev125267.service-now.com/'
    TESTENV = 'https://dev121163.service-now.com/'
    PRODENV = 'https://dev75867.service-now.com/'
    TESTSUITEID = '845f8b900b20220050192f15d6673aee'
  }
  stages {
    stage('Build') {
      when {
        not {
          branch 'master'
        }
      }
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")

      }
    }
    stage('Test') {
      when {
        not {
          branch 'master'
        }
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}")
        snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
      }
    }
    stage('Deploy to Prod') {
      when {
        branch 'master'
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${PRODENV}", appSysId: "${APPSYSID}")
      }
    }
  }
}
