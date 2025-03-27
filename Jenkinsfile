pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine' // Use Node.js 18 Alpine image
                    reuseNode true
                    args "--volume \"${WORKSPACE}\":/workspace --workdir /workspace"
                }
            }
            steps {
                sh '''
                echo "🚀 Running Build Inside Docker Container"

                echo "📂 Checking Workspace Files"
                ls -la

                echo "🛠️ Node.js & npm Versions"
                node --version
                npm --version

                echo "📦 Installing Dependencies"
                if [ -f package-lock.json ]; then
                    npm ci
                else
                    npm install
                fi

                echo "🏗️ Running Build"
                npm run build || echo "❌ Build failed"

                echo "📂 Final Directory Structure"
                ls -la 
                '''
            }
        }
    }
}
