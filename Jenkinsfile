pipeline {
    agent any

    stages {
        stage('Clean up the project') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('Build, test and publish') {
            steps {
                sh 'mvn package'
            }
        }

        stage('publish the test results') {
            steps {
                junit 'target/surefire-reports/*.xml'
            }
        }

        stage('publish artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

    }
}