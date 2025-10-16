pipeline {
    agent {label 'srv1-zakaria'}
    stages {
        stage('Checkout SCM') {
            steps {git branch: 'main', url: 'https://github.com/zaxrmdn/simple-apps-2.git'}
        }
        stage('Build') {
            steps {
                sh '''cd apps
                npm install'''
            }
        }
        stage('Testing') {
            steps {
                sh '''cd apps
                npm test
                npm run test:coverage'''
            }
        }
        stage('Code Review') {
            steps {
                sh '''cd apps
                sonar-scanner \
                 -Dsonar.projectKey=simple-apps \
                 -Dsonar.sources=. \
                 -Dsonar.host.url=http://172.23.7.214:9000 \
                 -Dsonar.login=sqp_64963812aac8dde1ca7ac98f74fa55fe3f2925a3'''
            }
        }
        stage('Deploy compose') {
            steps {
                sh '''
                docker compose build
                docker compose up -d
                '''
            }
        }
    }
}