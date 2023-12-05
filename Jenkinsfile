pipeline {
    agent any

    stages {
        stage('Clean up the project') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('Run Sonarqube analysis') {
            steps {
                withSonarQubeEnv('sonar') {
      sh "mvn clean verify sonar:sonar -Dsonar.projectKey=sample-java-app -Dsonar.projectName='sample-java-app'"
    }
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