pipeline {
    agent any

    environment {
        IMAGE_NAME = "fastapi"
        CONTAINER_NAME = "fastapi_container"
        APP_PORT = "8000"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/SamhithaSingirikonda/fastapi-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME} .'  // ✅ Use ${} inside strings
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker run -d --name ${CONTAINER_NAME} -p ${APP_PORT}:${APP_PORT} ${IMAGE_NAME}
                '''
            }
        }
    }
}
