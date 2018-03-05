pipeline {
    agent { 
      docker { 
        image 'node:6.3' 
      }
    }
    stages {
        stage('build') {
            steps {
              sh 'npm --version'
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
    }
}
