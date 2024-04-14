pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/sainadh30/nodejs.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'docker build . -t sai3009/my-node-js-app:latest'
            }
        }
        stage('Push to Docker Registry') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '5c0d3c6d-feb1-4653-8639-78e7215c1bb7', toolName: 'docker') {
                        sh 'docker push sai3009/my-node-js-app:latest'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '5c0d3c6d-feb1-4653-8639-78e7215c1bb7', toolName: 'docker') {
                        sh 'docker run -d --name nodetodoapp -p 3000:3000 sai3009/my-node-js-app:latest'
                    }
                }
            }
        }
    }
}
