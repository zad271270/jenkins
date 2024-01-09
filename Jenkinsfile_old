pipeline {

  agent any

  stages {

    stage(clone repo) {
      /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage (build) {
      steps {
        
        app = docker.build("dazarate1970/web1")
      }

    }

  }

}


      
