pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Compile and build your application
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                // Run JUnit tests
                sh './gradlew test'
            }
            post {
                always {
                    // Publish JUnit test results
                    junit 'build/test-results/test/*.xml'
                }
            }
        }
    }
}