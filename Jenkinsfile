pipeline {
  options { 
    //only keep logs for 5 runs
    buildDiscarder(logRotator(numToKeepStr: '5')) 
    //declarative does a checkout automatically, set this to disable
    skipDefaultCheckout()
  }
  agent {
    //we need Docker Compose in many of the sh steps
    //we want to use Docker-in-Docker (DIND) to isolate Docker Compose images, containers, networks from other running jobs
    label "master"
  }
  environment {
    env='test'
  }
  stages {
    stage("Prepare Build Environment") {
      steps {
        //checkout code for all stages - sharing agent across stages
        checkout scm
        //load docker image saved in agent - this speeds up the job almost 10x
        sh 'mvnw clean package'
      }
    }
  }
}
