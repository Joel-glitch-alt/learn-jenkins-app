pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                echo "Running Build Without Docker"

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
                npm run build || echo "Build failed"

                echo "Final Directory Structure"
                ls -la 
                '''
            }
        }
    }
}
