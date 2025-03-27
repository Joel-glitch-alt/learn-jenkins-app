pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    args '-v $WORKSPACE:/workspace -w /workspace'
                }
            }
            steps {
                sh '''
                echo "Checking Workspace Files"
                ls -la
                echo "Node.js & npm Versions"
                node --version
                npm --version

                echo "Installing Dependencies"
                if [ -f package-lock.json ]; then
                    npm ci
                else
                    npm install
                fi

                echo "Running Build"
                npm run build

                echo "Final Directory Structure"
                ls -la 
                '''
            }
        }
    }
}
