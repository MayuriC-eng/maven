pipeline {
    agent any

    tools {
        // Make sure these names EXACTLY match Jenkins → Manage Jenkins → Tools
        maven "Maven3"
        jdk "JDK-17"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Initialize') {
            steps {
                bat "echo PATH=%PATH%"
                bat "java -version"
                bat "mvn -version"
            }
        }

        stage('Build') {
            steps {
                bat "mvn -B clean package"
            }
        }

        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true,
                  testResults: '**/target/surefire-reports/*.xml'
        }
    }
}
