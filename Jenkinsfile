pipeline {
    agent any

    stages {
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=petclinic -Dsonar.projectName=petclinic'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Wait for the SonarQube quality gate result
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
