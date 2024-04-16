pipeline {
    agent any
    options {
        timeout(time: 120, unit: 'MINUTES')
    }
    stages {
        stage('Build') {
            withMaven() {
                steps {
                    sh 'mvn clean package'
                }
            }
        }
    }
}
