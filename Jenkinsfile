pipeline {
    agent any
    
    tools {
        // These names must match what you configured in Global Tool Configuration
        maven "MAVEN" 
        jdk "JDK"
    }

    stages {
        stage('Initialize') {
            steps {
                // On Windows, use 'bat' and Windows environment variable syntax
                bat "echo Current Path is %PATH%"
            }
        }
        
        stage('Build') {
            steps {
                // We removed the 'dir' block because Jenkins is already 
                // inside your workspace folder by default.
                bat 'mvn -B -DskipTests clean package'
            }
        }
    }
    
    post {
        always {
            // Updated pattern to standard Maven surefire report location
            junit(
                allowEmptyResults: true, 
                testResults: '**/target/surefire-reports/*.xml'
            )
        }
    }
}
