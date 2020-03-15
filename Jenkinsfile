pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean'
      }
    }

  }
  post {
    failure {
      sh "git bisect start ${BROKEN} ${STABLE}"
      sh 'git bisect run mvn clean test'
      sh 'git bisect reset'
    }

  }
}