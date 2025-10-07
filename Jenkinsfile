post {
    always {
        bat "docker ps -a"
    }
    cleanup {
        bat """
        docker stop %IMAGE_NAME%_%DEV_TAG% 
        exit /b 0
        """
        bat """
        docker stop %IMAGE_NAME%_%TEST_TAG% 
        exit /b 0
        """
        bat """
        docker rm %IMAGE_NAME%_%DEV_TAG% 
        exit /b 0
        """
        bat """
        docker rm %IMAGE_NAME%_%TEST_TAG% 
        exit /b 0
        """
    }
}
