pipeline {
    agent any

    stages {
        stage('checkout & build') {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_USER', variable: 'DOCKER_USER')]) {
                sh 'printenv'
                sh 'docker build -t $DOCKER_USER/web:latest -f Dockerfile .'
                }
            } 
        }
        
        stage('push to docker hub') {
            
            steps {
                withCredentials([string(credentialsId: 'DOCKER_USER', variable: 'DOCKER_USER'), string(credentialsId: 'DOCKER_PASSWD', variable: 'DOCKER_PASSWD')]) {
                sh 'docker login -u $DOCKER_USER -p $DOCKER_PASSWD'
                sh 'docker push $DOCKER_USER/web'
                }
            }
        }
    }
}
