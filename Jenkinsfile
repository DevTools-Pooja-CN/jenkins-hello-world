pipeline {
    agent any

    tools {

        maven 'M398'
    }

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
                // git branch: 'main', changelog: false, poll: false, url: 'https://github.com/Pooja-DevTools/jenkins-hello-world.git'
                sh 'mvn clean package -DskipTests=true'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }
    }
}
