pipeline {
    agent any

    environment {
        IMAGE_NAME = "rupesh2805/task1:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Login to Docker Hub & Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-login', usernameVariable: rupesh2805, passwordVariable: rupeshc@20)]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    sh '''
                        docker rm -f nodejs-demo-app || true
                        docker run -d -p 3000:3000 --name nodejs-demo-app $IMAGE_NAME
                    '''
                }
            }
        }
    }

    post {
        always {
            script {
                sh 'docker logout || true'
            }
        }
    }
}
