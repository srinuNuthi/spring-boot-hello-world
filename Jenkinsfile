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

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar_qube') {
                    sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=petclinic -Dsonar.projectName=petclinic'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
