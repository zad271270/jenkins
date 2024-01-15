pipeline {
    agent any

    stages {
        
        stage('CleanUp Workspace') {
            steps {
                cleanWs()
            }
            
        }
        
        stage('Checkout from SCM') {
            steps {
                
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/zad271270/jenkins'
            }
        }

                stage("Sonarqube Analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh "sonar-scanner   -Dsonar.projectKey=jenkins   -Dsonar.sources=.   -Dsonar.host.url=http://192.168.100.61:9000"
                    }
                }
            }

        }

        stage("Quality Gate") {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }

        }
        stage('Docker checkout & build') {
            steps {
                withCredentials([string(credentialsId: 'DOCKER_USER', variable: 'DOCKER_USER')]) {
                sh 'printenv'
                sh 'docker build -t $DOCKER_USER/web:latest -f Dockerfile .'
                }
            } 
        }
        
        stage('Push to docker hub') {
            
            steps {
                withCredentials([string(credentialsId: 'DOCKER_USER', variable: 'DOCKER_USER'), string(credentialsId: 'DOCKER_PASSWD', variable: 'DOCKER_PASSWD')]) {
                sh 'docker login -u $DOCKER_USER -p $DOCKER_PASSWD'
                sh 'docker push $DOCKER_USER/web'
                }
            }
        }
    }
}