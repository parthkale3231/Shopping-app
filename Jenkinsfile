pipeline {
    agent any

    environment {
        PROJECT_NAME = "ShopingKaro"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'master',
                url: 'https://github.com/parthkale3231/Shopping-app.git'
            }
        }

        stage('Stop Existing Containers') {
            steps {
                sh 'docker compose down || true'
            }
        }

        stage('Build Containers') {
            steps {
                sh 'docker compose up --build -d'
            }
        }

        stage('Check Running Containers') {
            steps {
                sh 'docker ps'
            }
        }


         stage('Wait for Application Startup') {
            steps {
                sh 'sleep 60'
            }
        }

        stage('Application Health Check') {
            steps {
                sh 'curl -f http://localhost:3000 || exit 1'
            }
        }
    }

    post {

        success {
            echo 'ShopingKaro CI Pipeline Executed Successfully!'
        }

        failure {
            echo 'Pipeline Failed!'
        }
    }
}
