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
        sh 'mvn test'
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