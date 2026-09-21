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
                sh 'javac src/Main.java'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'java -cp src Main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-cicd-app:${BUILD_NUMBER} .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f jenkins-cicd-container || true
                    docker run --name jenkins-cicd-container jenkins-cicd-app:${BUILD_NUMBER}
                '''
            }
        }
    }
}