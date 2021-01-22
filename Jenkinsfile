pipeline {
  options { 
    //only keep logs for 5 runs
    buildDiscarder(logRotator(numToKeepStr: '5')) 
    //declarative does a checkout automatically, set this to disable
    
  }
  agent {
    //we need Docker Compose in many of the sh steps
    //we want to use Docker-in-Docker (DIND) to isolate Docker Compose images, containers, networks from other running jobs
    label "master"
  }
  environment {
    env='test'
  }
  parameters {
        choice(name: 'Branch', choices: Nirmit)
  }
  stages {

    stage("Prepare Build Environment") {
      steps {
        scripts {
          sh 'mvnw clean package'
        }
      }
    }
    
    stage("Publish Build Environment") {
      steps {
        scripts {
           echo "rtPublish"
        }
      }
    }
    
    stage("AWS Deploy") {
      steps {
        scripts {
           echo "aws cloudformation cftemplate.json"
        }
      }
    }
  }
}
