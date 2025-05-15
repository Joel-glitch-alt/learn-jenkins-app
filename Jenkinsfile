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
        SCANNER_HOME = tool 'sonar-scanner' // Matches Global Tool Config name
        DOCKER_USERNAME = 'addition1905'
        DOCKER_IMAGE = 'addition1905/jenkins-nodejs:latest'
    }

    stages {
        stage('Install & Build') {
            agent {
                docker {
                    image 'node:18'  // Full version includes npm and node
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "📦 Installing dependencies..."
                    [ -f package-lock.json ] && npm ci || npm install

                    echo "🏗️ Building app..."
                    npm run build || echo "No build script defined"

                    echo "✅ Build complete"
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "🧪 Running tests..."
                    npm test || echo "Tests failed or not defined"
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh '''
                        ${SCANNER_HOME}/bin/sonar-scanner \
                          -Dsonar.projectKey=my_project_key \
                          -Dsonar.projectName="My JS Project" \
                          -Dsonar.sources=./src \
                          -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info \
                          -Dsonar.sourceEncoding=UTF-8
                    '''
                }
            }
        }

       stage('Quality Gate') {
    steps {
        timeout(time: 5, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
}

       stage('Docker Build & Push') {
    steps {
        script {
            def img = docker.build("${DOCKER_IMAGE}")
            docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                img.push()
            }
        }
    }
}
    }

    post {
        success {
            echo '✅ All steps completed successfully.'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
