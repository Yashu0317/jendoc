pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        DEV_TAG = "dev"
        TEST_TAG = "test"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Yashu0317/jendoc.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Run Dev Container') {
            steps {
                bat "docker run -d -p 3000:3000 --name %IMAGE_NAME%_%DEV_TAG% %IMAGE_NAME%"
            }
        }

        stage('Run Test Container') {
            steps {
                bat "docker run -d -p 4000:3000 --name %IMAGE_NAME%_%TEST_TAG% %IMAGE_NAME%"
            }
        }
    }

    post {
        always {
            bat "docker ps -a"
        }
        cleanup {
            bat "docker stop %IMAGE_NAME%_%DEV_TAG% || true"
            bat "docker stop %IMAGE_NAME%_%TEST_TAG% || true"
            bat "docker rm %IMAGE_NAME%_%DEV_TAG% || true"
            bat "docker rm %IMAGE_NAME%_%TEST_TAG% || true"
        }
    }
}
