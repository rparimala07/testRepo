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
    stage('Upload to S3') {
      steps {
        bat(script: '"C:\\Program Files\\Amazon\\AWSCLI\\aws.exe" s3 cp server\\target\\demo-0.0.1-SNAPSHOT.jar s3://artifact-repo-git/', returnStdout: true, returnStatus: true)
      }
    }
  }
}