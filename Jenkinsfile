pipeline {

  agent any

  stages {

    stage (build) {
      steps {
        sh 'printenv'
        sh 'docker build -t dazarate1970/web -f Dockerfile .'
      }

      stage('Docker Push') {
    	agent any
      steps {
      	withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push dazarate1970/web:latest'
        }
      }
    }

    }

  }

}


      
