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
      environment {
        JAVA_HOME = 'C:\\Program Files (x86)\\Java\\jdk1.8.0_171'
      }
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
      environment {
        AWS_SHARED_CREDENTIALS_FILE = 'C:\\Users\\Owner\\.aws\\credentials'
      }
      steps {
        bat(script: '"C:\\Program Files\\Amazon\\AWSCLI\\aws.exe" --region us-west-1 s3 cp server\\target\\demo-0.0.1-SNAPSHOT.jar s3://artifact-repo-git/', returnStdout: true, returnStatus: true)
      }
    }
    stage('Deploy') {
      environment {
        AWS_SHARED_CREDENTIALS_FILE = 'C:\\Users\\Owner\\.aws\\credentials'
      }
      steps {
        bat(script: '"C:\\Program Files\\Amazon\\AWSCLI\\aws.exe" --region us-west-1 cloudformation create-stack --stack-name myteststack --template-body file://template.yaml', returnStatus: true, returnStdout: true)
      }
    }
  }
}