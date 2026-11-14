pipeline {
    agent any
    environment {
        DOCKER_ID  = 'algo04'
        BACKEND    = "${DOCKER_ID}/nxttrendz-backend"
        FRONTEND   = "${DOCKER_ID}/nxttrendz-frontend"
        EC2_HOST   = '35.154.230.22'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/VaibhavWadagale1/Ecomtrendz'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t $BACKEND:$BUILD_NUMBER ./backend'
                sh 'docker build -t $FRONTEND:$BUILD_NUMBER ./frontend'
            }
        }
        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-crediatials',
                    usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $BACKEND:$BUILD_NUMBER'
                    sh 'docker push $FRONTEND:$BUILD_NUMBER'
                }
            }
        }
    }
}