pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Vishnu-V-N/ci-cd-pipeline-jenkins-nodejs.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t ci-cd-app .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                bat '''
                @echo off
                for /f %%i in ('docker ps -q --filter "ancestor=ci-cd-app"') do (
                    echo Stopping container ID: %%i
                    docker rm -f %%i
                )
                echo Done stopping containers.
                '''
            }
        }

        stage('Debug Docker') {
            steps {
                bat '''
                echo Checking Docker environment...
                whoami
                docker --version
                docker ps -a
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 3000:3000 ci-cd-app'
            }
        }
    }
}
