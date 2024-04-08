pipeline {
    agent any
    // tools (nodejs "nodejs")
    stages {
        stage('Clone Repository'){
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
                withDockerRegistry(credentialsId: '7eb82be1-8078-4675-bf04-eae50181f633') {
                    sh 'docker push sai3009/my-node-js-app:latest'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo docker run -d --name nodetodoapp -p 3000:3000 sai3009/my-node-js-app:latest'
            }
        }
    }
}
