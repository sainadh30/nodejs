pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS = '5c0d3c6d-feb1-4653-8639-78e7215c1bb7'
        DOCKER_IMAGE = 'sai3009/my-node-js-app:latest'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/sainadh30/nodejs.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'docker build . -t $DOCKER_IMAGE'
            }
        }
        stage('Push to Docker Registry') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_CREDENTIALS) {
                        sh 'docker push $DOCKER_IMAGE'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d --name nodetodoapp -p 3000:3000 $DOCKER_IMAGE'
            }
        }
    }
}
