pipeline {
    agent {
      docker {
        image 'node:6.3'
        // image 'node:7-alpine'
      }
      parameters {
        password( name: 'AWS_ACCESS_KEY_ID', defaultValue: '', description: 'AWS Access Key')
        password( name: 'AWS_SECRET_ACCESS_KEY', defaultValue: '', description: 'AWS Secret Key')
        choice( choices: 'dev\nqa', description: 'Please select environment to deploy to', name: 'ENV')
      }
    }
    stages {
        stage('build') {
            steps {
              sh 'npm --version'
              sh 'node --version'
              sh 'echo "Hello World"'
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
