pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/nihalsingh571/sudokusolver.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t sudokusolver-image .'
                }
            }
        }

        stage('Stop Previous Container') {
            steps {
                script {
                    sh 'docker stop sudokusolver-container || true'
                    sh 'docker rm sudokusolver-container || true'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -d --name sudokusolver-container -p 3000:3000 sudokusolver-image'
                }
            }
        }
    }

    post {
        failure {
            echo 'Build failed!'
        }
    }
}
