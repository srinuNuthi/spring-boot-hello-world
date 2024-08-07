pipeline {
    agent any 
    stages {
        stage ('vcs') {
           steps {
             git  url: 'https://github.com/srinuNuthi/spring-boot-hello-world.git',
                 branch: main
           }
        }
        stage ('package') {
            steps {
            sh 'mvn clean package'
            }
        }
    }
}
