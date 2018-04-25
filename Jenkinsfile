pipeline {
  agent any
  stages {
    stage('Build') {
      environment {
        JAVA_HOME = 'C:\\Program Files (x86)\\Java\\jdk1.8.0_171'
      }
      steps {
        bat(script: 'cd server && mvnw package', returnStdout: true, returnStatus: true)
      }
    }
    stage('Test') {
      steps {
        bat(script: 'cd server && mvnw test', returnStatus: true, returnStdout: true)
      }
    }
    stage('Archive Artifact') {
      steps {
        archiveArtifacts 'server\\target\\*'
      }
    }
  }
}