pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/tempat-belajar/simple-deploy-test.git',
                    credentialsId: 'simple-deploy'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t simple-web:latest .'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh '''
                    docker ps -q --filter "name=simple-web" | grep -q . && docker stop simple-web && docker rm simple-web || true
                    docker run -d --name simple-web -p 8085:80 simple-web:latest
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "🚀 Deployment success! Akses di http://<server_ip>:8085"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
