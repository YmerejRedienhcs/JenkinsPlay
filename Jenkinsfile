pipeline {
    agent {
      docker {
        image 'node:6.3'
        // image 'node:7-alpine'
      }
    }
    parameters {
      password( name: 'AWS_ACCESS_KEY_ID', defaultValue: '', description: 'AWS Access Key')
      password( name: 'AWS_SECRET_ACCESS_KEY', defaultValue: '', description: 'AWS Secret Key')
      choice( choices: 'dev\nqa', description: 'Please select environment to deploy to', name: 'DEPLOY_ENV')
    }

    environment {
      TUTORIAL_GLOBAL_ENV_VAR_1 = 'true'
    }

    stages {
      stage('build') {
        environment {
          TUTORIAL_BUILD_STAGE_ENV_VAR_1 = 'true'
        }
        steps {
          sh 'echo "Hello, World, we are building"'
          sh 'printenv'
          sh 'npm --version'
          sh 'node --version'
          sh '''
            echo "Multiline shell steps works too"
            ls -lah
          '''
          timeout(time: 1, unit: 'MINUTES') {
            retry(3) {
              sh 'date'
              sh 'sleep 10'
              sh 'curl jeredith.com/jenkinstest.html 2>/dev/null | grep success'
            }
          }
        }
      }
      stage('deploy') {
        environment {
          TUTORIAL_DEPLOY_STAGE_ENV_VAR_1 = 'true'
        }
        steps {
          sh 'echo "Hello World, we are deploying."'
          sh 'printenv'
          sh 'npm --version'
          sh 'node --version'
        }
      }

    }
    post {
      always {
        echo 'This always runs after stages'
      }
      success {
        echo 'Success after stages!'
      }
      unstable {
        echo 'Ruh-roh -- getting unstable!'
      }
      changed {
        echo 'Pipeline state has changed...'
      }
    }
}
