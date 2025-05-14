// pipeline {
//     agent any

//     stages {
//         stage('w/o docker') {
//             steps {
//                 sh 'echo "Without Docker"'
//             }
//         }

//         stage('w/ docker') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     reuseNode true   // ✅ correctly placed
//                 }
//             }
//             steps {
//                 sh 'echo "With Docker"'
//                 sh 'npm --version'
//             }
//         }
//     }
// }


// pipeline {
//     agent any
//     stages {
//         stage('Build') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     reuseNode true   // ✅ correctly placed
//                 }
//             }
//             steps {
//                 //echo 'Hello World'
//                 sh '''
//                     ls -la
//                     node --version
//                     npm --version
//                     npm ci
//                     npm run build
//                     ls -la
//                 '''
//             }
//         }
        
//         stage ('Test') {
//             agent {
//                 docker {
//                     image 'node:18-alpine'
//                     reuseNode true
//                 }
//             }

//             steps {
//                 sh '''
//                 test -f build/index.html
//                 npm test
//                 '''
//             }
//         }
//     }
     
//   //Code Quality
//     post {
//         always {
//             junit 'test-results/junit.xml'
//         }
//     }
// }

pipeline {
    agent any

    environment {
        SCANNER_HOME = tool 'sonar-scanner'
        DOCKER_USERNAME = 'addition1905'
        DOCKER_IMAGE = 'addition1905/jenkins-nodejs:latest'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh "${SCANNER_HOME}/bin/sonar-scanner"
                }
            }
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}

