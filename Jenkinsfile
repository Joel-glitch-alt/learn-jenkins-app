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


pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true   // ✅ correctly placed
                }
            }
            steps {
                //echo 'Hello World'
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
        
        stage ('Test') {
            steps {
                sh 'test -f build/index.html'
            }
        }
    }
}
