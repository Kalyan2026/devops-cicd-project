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
        stage('Update Deployment Manifest') {
            steps {
                sh '''
                sed -i "s|image:.*|image: kalyandevops2026/devops-cicd-project:${BUILD_NUMBER}|g" k8s/deployment.yaml

                git config --global user.email "kalyandevops2026@gmail.com"
                git config --global user.name "kalyan2026"

                git add k8s/deployment.yaml
                git commit -m "Updated image tag to ${BUILD_NUMBER}" || true
                '''
            }
        }
        stage('Push Manifest Changes') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'github-creds',
                        usernameVariable: 'GIT_USER',
                        passwordVariable: 'GIT_PASS'
                    )
                ]) {

                    sh '''
                    git remote set-url origin https://${GIT_USER}:${GIT_PASS}@github.com/Kalyan2026/devops-cicd-project.git

                    git push origin main
                    '''
                }
            }
        }
    }
}