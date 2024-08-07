pipeline {
    agent any

    stages {
        stage('Package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Print JUnit Results') {
            steps {
                junit allowEmptyResults: false, testResults: '**/target/surefire-reports/*.xml'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar',
                               allowEmptyArchive: true,
                               fingerprint: true,
                               onlyIfSuccessful: true
            }
        }
    }
}
