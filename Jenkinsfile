pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh '''
                 docker build -t kalyandevops2026/devops-cicd-project:${BUILD_NUMBER} app/
                 '''
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([
                    usernamePassword(
                      credentialsId: 'dockerhub-creds',
                      usernameVariable: 'DOCKER_USER',
                      passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    '''
                }
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push kalyandevops2026/devops-cicd-project:${BUILD_NUMBER}'
            }
        }
    }
}