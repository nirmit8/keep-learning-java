pipeline {
  agent none
  options { 
    //only keep logs for 5 runs
    buildDiscarder(logRotator(numToKeepStr: '5')) 
    //declarative does a checkout automatically, set this to disable
    
  }
  environment {
    env='test'
  }
  parameters {
        choice(name: 'Branch', choices: Nirmit)
  }
  stages {

    stage("Prepare Build Environment") {
      agent { label "maven" }
      steps {
        scripts {
          sh 'mvnw clean package'
        }
      }
    }
    
    stage("Publish Build Environment") {
      agent { label "nodejs" }
      steps {
        scripts {
           echo "npm install"
        }
      }
    }
    
    stage("AWS Deploy") {
      agent { label "deploy" }
      steps {
        scripts {
           echo "aws cloudformation cftemplate.json"
        }
      }
    }
  }
}
