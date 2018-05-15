pipeline {
  agent none
  environment {
    NODE_VER = '8.1.0'
  }

  post {
    success {
      echo 'succees'
    }
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

    stage('Deploy to stage?') { agent none
      when {
        anyOf {
          branch 'stage'
          environment name: 'NODE_VER', value: '8.1.0'  
        }
      }
      steps {
        input 'Deploy to stage?'
      }
    }

    stage('Parallel') {
      failFast true
      parallel {
        stage('Build 1') { agent any
          steps {
            echo "Its ME!"
          }
        }
        
        stage('Build 2') { agent any
          steps {
            echo "Not ME!"
          }
        }
      }    
    }
  }
}
