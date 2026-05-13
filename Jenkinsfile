pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'Docker-credentials'
        IMAGE_NAME = 'pannu27/new_docker_image'
    }

    stages {

        stage('Build Java Application') {
            steps {
                bat 'javac Hello.java'
            }
        }

        stage('Run Java Program') {
            steps {
                bat 'java Hello'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                credentialsId: 'Docker-credentials',
                usernameVariable: 'USER',
                passwordVariable: 'PASS')]) {

                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%:latest'
            }
        }
    }
}
