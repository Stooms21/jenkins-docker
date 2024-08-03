pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('stooms-dockerhub')
    }
    stages {
        stage('Build docker image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        sh 'docker build -t myapp/flask:8 .'
                    }
                }
            }
        }
        stage('Login to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'
                    }
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        sh 'docker push myapp/flask:8'
                    }
                }
            }
        }
    }
}

