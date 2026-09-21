pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                bat 'javac src\\Main.java'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'java -cp src Main'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t jenkins-cicd-app:%BUILD_NUMBER% .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker rm -f jenkins-cicd-container 2>nul || exit /b 0'
                bat 'docker run --name jenkins-cicd-container jenkins-cicd-app:%BUILD_NUMBER%'
            }
        }
    }
}