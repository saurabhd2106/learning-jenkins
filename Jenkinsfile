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
               sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=sample-java-app \
  -Dsonar.projectName=\'sample-java-app\' \
  -Dsonar.host.url=http://20.163.158.43:81 \
  -Dsonar.token=sqp_0b3cbf84d5510b6e4479fc5aae1e09c9392538c5'
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