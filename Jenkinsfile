pipeline {
    agent any

    stages {
        
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