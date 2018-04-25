pipeline {
  agent any
  stages {
    stage('Build') {
      environment {
        JAVA_HOME = 'C:\\Program Files (x86)\\Java\\jdk1.8.0_171'
      }
      steps {
        bat 'mvnw package'
      }
    }
  }
}