pipeline {
    agent any 
    stages {
        stage ('vcs') {
            git  url: 'https://github.com/srinuNuthi/spring-boot-hello-world.git',
                 branch: main
        }
        stage ('package') {
            sh 'mvn clean package'
        }
    }
}
