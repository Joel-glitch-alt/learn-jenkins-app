pipeline {
    agent any


//   stages {
//         stage('Check Docker') {
//             steps {
//                 script {
//                     sh 'docker --version'  // This checks if docker is available
//                 }
//             }
//         }
//     }
    /////

    stages {
        stage('Without Docker') {
            steps {
                echo 'This is outside Docker'
            }
        }

    //     stage('With Docker') {
    //         agent {
    //             docker {
    //                 image 'node:18-alpine'
    //                 args '-u root'
    //             }
    //         }
    //         steps {
    //             sh '''
    //                 echo "Inside Docker"
    //                 node -v
    //                 npm -v
    //             '''
    //         }
    //     }
    // }
}
