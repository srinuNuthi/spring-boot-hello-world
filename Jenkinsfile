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
                withSonarQubeEnv('My SonarQube Server') {
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
        stage(' upload artifact to s3') {
            steps {
                ss3Upload consoleLogLevel: 'INFO',
                 dontSetBuildResultOnFailure: false,
                  dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'cf-templates-uh6slohihg2z-us-east-1', excludedFile: '', flatten: true, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: true, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: '**/target/*.jar', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: true]], 
                  pluginFailureResultConstraint: 'FAILURE',
                   profileName: 'my_s3_profile', userMetadata: []
            }
        }
    }
}

