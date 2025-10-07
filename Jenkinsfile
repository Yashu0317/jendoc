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
                git branch: 'main', url: 'https://github.com/Yashu0317/jendoc.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:%DEV_TAG% ."
                bat "docker tag %IMAGE_NAME%:%DEV_TAG% %IMAGE_NAME%:%TEST_TAG%"
            }
        }

        stage('Run Dev Container') {
            steps {
                bat "docker run -d -p 3000:3000 --name %IMAGE_NAME%_%DEV_TAG% %IMAGE_NAME%:%DEV_TAG%"
            }
        }

        stage('Run Test Container') {
            steps {
                bat "docker run -d -p 4000:3000 --name %IMAGE_NAME%_%TEST_TAG% %IMAGE_NAME%:%TEST_TAG%"
            }
        }
    }

    post {
        always {
            bat "docker ps -a"
        }
        cleanup {
            bat "docker stop %IMAGE_NAME%_%DEV_TAG% || exit /b 0"
            bat "docker stop %IMAGE_NAME%_%TEST_TAG% || exit /b 0"
            bat "docker rm %IMAGE_NAME%_%DEV_TAG% || exit /b 0"
            bat "docker rm %IMAGE_NAME%_%TEST_TAG% || exit /b 0"
        }
    }
}
