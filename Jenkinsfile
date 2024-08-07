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
    }
}
