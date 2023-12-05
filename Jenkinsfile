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
      sh "mvn clean verify sonar:sonar \
      -Dsonar.projectKey=sample-java-app \
      -Dsonar.projectName='sample-java-app' \
      -Dsonar.token='sqp_92cc315e1b3e2330ae44e72fe0e1aa94c27a18a4'"
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