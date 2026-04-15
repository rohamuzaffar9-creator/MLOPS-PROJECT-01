pipeline {
    agent any

    environment {
        IMAGE_NAME = "mlops-app"
        CONTAINER_NAME = "mlops-container"
        REPO_URL = "https://github.com/rohamuzaffar9-creator/MLOPS-PROJECT-01.git"
        BRANCH = "main"
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'

                git branch: "${BRANCH}",
                    url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t mlops-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                echo 'Stopping old container...'
                sh 'docker stop mlops-container || true'
                sh 'docker rm mlops-container || true'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running container...'
                sh 'docker run -d -p 8080:80 --name mlops-container mlops-app'
            }
        }
    }

    post {
        success {
            echo 'PIPELINE SUCCESS ✅'
        }

        failure {
            echo 'PIPELINE FAILED ❌'
        }
    }
}
