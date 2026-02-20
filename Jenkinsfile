pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SujalKishore/loginpage.git'
            }
        }

        stage('Setup Environment') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build & Deploy') {
            steps {
                bat 'docker compose down || exit /b 0'
                bat 'docker compose up -d --build'
            }
        }

        stage('Health Check') {
            steps {
                sleep time: 20, unit: 'SECONDS'
                bat 'powershell -Command "try { Invoke-WebRequest http://localhost:3000 -UseBasicParsing } catch { exit 1 }"'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}