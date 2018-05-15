pipeline {
  agent none
  environment {
    NODE_VER = '8.1.0'
  }
  stages {
    stage('Beginning') { agent any
      environment {
        DEPLOY_VERSION = 'stage'
      }
      steps {
        echo 'Hello world'
        sh 'echo $NODE_VAR'
        echo "${env.DEPLOY_VERSION}"
      }
    }

    stage('Who am I?') { agent any 
      environment {
          DEPLOY_VERSION = 'prod'
      }
      steps {
        echo "${env.DEPLOY_VERSION}"
        sh 'host -t TXT pgp.michaelholley.us |awk -F \'"\' \'{print $2}\''
      }
    }

    stage('Deploy to stage?') { agent any
      steps {
        input 'Deploy to stage?'
      }
    }
  }
}
