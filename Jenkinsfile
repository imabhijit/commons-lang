pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test -Drat.numUnapprovedLicenses=15'
      }
    }

  }
  post {
    failure {
      sh "git bisect start ${BROKEN} ${STABLE}"
      sh 'git bisect run mvn clean test -Drat.numUnapprovedLicenses=15'
      sh 'git bisect reset'
    }

  }
}
