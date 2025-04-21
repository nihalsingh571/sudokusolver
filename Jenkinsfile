pipeline {
    agent any

    environment {
        IMAGE_NAME = "sudokusolver"
        CONTAINER_NAME = "sudoku-container"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/nihalsingh571/sudokusolver.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Stop Previous Container') {
            steps {
                sh "docker stop $CONTAINER_NAME || true"
                sh "docker rm $CONTAINER_NAME || true"
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $IMAGE_NAME"
            }
        }
    }

    post {
        success {
            echo "App is running at http://localhost:${PORT}"
        }
        failure {
            echo "Build failed!"
        }
    }
}
