pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling code from GitHub...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t devsecops-demo .'
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running container...'
                sh 'docker run -d -p 5000:5000 --name devsecops-demo devsecops-demo'
            }
        }

        stage('Verify App') {
            steps {
                echo 'Listing running containers...'
                sh 'docker ps'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker stop devsecops-demo || true'
            sh 'docker rm devsecops-demo || true'
        }
    }
}
