pipeline {
    agent any

    stages {
        stage('Without Docker') {
            steps {
                echo 'This is outside Docker'
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u root'
                    reuseNode true
                }
            }
            steps {
                sh '''
                test -f build/index.html && echo "File exists" || echo "File does not exist"
                npm test  # Ensure your test command generates a JUnit report
                '''
            }
        }

        // Optionally include a stage for "With Docker"
        // stage('With Docker') {
        //     agent {
        //         docker {
        //             image 'node:18-alpine'
        //             args '-u root'
        //         }
        //     }
        //     steps {
        //         sh '''
        //             echo "Inside Docker"
        //             node -v
        //             npm -v
        //         '''
        //     }
        // }

    }

    post {
        always {
            // Publish the JUnit test results from the generated XML
            junit '**/test-results/junit.xml'
        }
    }
}
