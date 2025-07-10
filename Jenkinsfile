pipeline {
  agent any
  stages {
    stage('Echo Version') {
      steps {
        sh 'echo Print Maven Version'
        sh 'mvn -version'
        sh 'java -version'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests=true'
        archiveArtifacts 'target/hello-demo-*.jar'
      }
    }

    stage('Unit Test') {
      post {
        always {
          junit '**/target/surefire-reports/*.xml'
          archiveArtifacts(artifacts: 'target/*.jar', fingerprint: true)
        }

      }
      steps {
        sh 'mvn test'
      }
    }

  }
  tools {
    maven 'M398'
  }
}