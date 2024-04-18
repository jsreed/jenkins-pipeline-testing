pipeline {
    agent any
    options { 
        preserveStashes(buildCount: 1) 
    } 
    parameters {
        booleanParam(name: 'IS_RELEASE_BUILD', defaultValue: false, description: 'Whether or not to a perform mvn release.')
    }
    stages {
        stage('Build') {
            steps {
                echo "Building..."
                echo "IS_RELEASE_BUILD=${params.IS_RELEASE_BUILD}"
                withMaven(maven: 'mvn-3.9.6') {
                    sh "mvn clean package"
                }
            }
        }
        stage('Validate') {
            steps {
                echo "Validating..."
                echo "IS_RELEASE_BUILD=${params.IS_RELEASE_BUILD}"
                withSonarQubeEnv('Sonar') {
                    withMaven(maven: 'mvn-3.9.6') {
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }
        stage('Release') {
            steps {
                echo "Releasing..."
            }
        }
    }
}
