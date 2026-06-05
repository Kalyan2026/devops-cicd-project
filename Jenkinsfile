pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https:..github.com/Kalyan2026/devops-cicd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-cicd-project:v1 app/'
            }
        }

        stage('List Images') {
            steps {
                sh 'docker images'
            }
        }
    }
}