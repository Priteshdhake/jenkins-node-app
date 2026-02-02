pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Priteshdhake/jenkins-node-app.git',
                    credentialsId: 'gitHubCred'
            }
        }

        stage('Install Dependencies & Test') {
            agent {
                docker {
                    image 'node:18'
                    args '-u root:root'
                }
            }
            steps {
                sh 'npm install'
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-node-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker rm -f jenkins-node-app-container || true'
                sh 'docker run -d -p 3000:3000 --name jenkins-node-app-container jenkins-node-app'
            }
        }
    }
}
