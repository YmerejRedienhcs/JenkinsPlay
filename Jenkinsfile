pipeline {
    agent {
      docker {
        image 'node:6.3'
        // image 'node:7-alpine'
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
