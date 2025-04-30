pipeline {
    agent any

     stages {
        stage('Without Docker') {
            steps {
                echo 'This is outside Docker'
                dir('.') {
                    echo "Current directory: ${pwd()}"
                }
            }
        }
    }

    //     stage('w/ docker') {
    //         agent {
    //             docker {
    //                 image 'node:18-alpine'
    //                 args '-u root' // Run as root if permission issues occur
    //             }
    //         }
    //         steps {
    //             sh '''
    //                 echo "With Docker"
    //                 node -v
    //                 npm -v
    //             '''
    //         }
    //     }
    // }
}
