// '''
// pipeline {
//     agent any

//     stages {
//         stage('Without Docker') {
//             steps {
//                 echo 'This is outside Docker'
//             }
//         }

//          //Using Docker
//         stage('Test') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     args '-u root'
//                     reuseNode true
//                 }
//             }
//             steps {
//                 sh '''
//                 test -f build/index.html && echo "File exists" || echo "File does not exist"
//                 npm test  # Ensure your test command generates a JUnit report
//                 '''
//             }
//         }

//         // Optionally include a stage for "With Docker"
//         // stage('With Docker') {
//         //     agent {
//         //         docker {
//         //             image 'node:18-alpine'
//         //             args '-u root'
//         //         }
//         //     }
//         //     steps {
//         //         sh '''
//         //             echo "Inside Docker"
//         //             node -v
//         //             npm -v
//         //         '''
//         //     }
//         // }

//     }

//     post {
//         always {
//             // Publish the JUnit test results from the generated XML
//             junit '**/test-results/junit.xml'
//         }
//     }
// }
// '''

pipeline {
    agent any

    stages {
        stage('Install Docker CLI') {
            steps {
                script {
                    // Installing Docker CLI inside the agent
                    sh '''
                    apt-get update
                    apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release
                    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
                    echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
                    apt-get update
                    apt-get install -y docker-ce-cli
                    '''
                }
            }
        }

        stage('Test Docker Installation') {
            steps {
                script {
                    // Verify Docker CLI installation
                    sh 'docker --version'
                }
            }
        }

        stage('Run Docker Command') {
            steps {
                script {
                    // Now you can run docker commands
                    sh 'docker ps'
                }
            }
        }
    }
}
