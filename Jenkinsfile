pipeline {
  agent {
      label 'build'
  }
  stages {
    stage ('Build') {
      steps {
      sh 'rm -rf ./cypress'
      sh '''
        npm install
        npm run build
        sudo npm install -g serve
        serve -s build &
        '''
      }
    }
    stage ('Test') {
      agent {
        label 'test'
      }
      steps {
      sh ''' 
        npm install cypress
        npm install mocha
        npx cypress run --spec ./cypress/integration/test.spec.js
        '''
      }
      post {
        always {
          junit 'results/cypress-report.xml'
        }
          
      }
    }
  }
} 
