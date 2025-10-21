pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo '🛠️ Building Docker Image...'
                sh 'docker build -t simple-web:latest .'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying container...'
                sh 'docker run -d --name simple-web -p 8081:80 simple-web:latest || true'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
