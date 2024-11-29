pipeline {
    agent any

    environment {
        APP_NAME = "flask_app"
        CONTAINER_PORT = "80"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t ${APP_NAME}:latest .'
                }
            }
        }

        stage('Remove Old Container') {
            steps {
                script {
                    sh '''
                    docker ps -q --filter "name=${APP_NAME}" | xargs -r docker stop
                    docker ps -aq --filter "name=${APP_NAME}" | xargs -r docker rm
                    '''
                }
            }
        }

        stage('Run New Container') {
            steps {
                script {
                    sh '''
                    docker run -d --name ${APP_NAME} -p ${CONTAINER_PORT}:5000 ${APP_NAME}:latest
                    '''
                }
            }
        }
    }
}
