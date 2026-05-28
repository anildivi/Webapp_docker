pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-nginx-app"
        CONTAINER_NAME = "nginx-container"
    }

    stages {

        stage('Clone GitHub Repository') {
            steps {
                git 'https://github.com/anildivi/Webapp_docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker run -d \
                --name $CONTAINER_NAME \
                -p 80:80 \
                $IMAGE_NAME
                '''
            }
        }

        stage('Verify Container') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
