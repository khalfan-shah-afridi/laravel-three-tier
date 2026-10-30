pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'khalfan-shah-afridi/laravel-app'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/khalfan-shah-afridi/laravel-three-tier.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully! Application is live.'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
