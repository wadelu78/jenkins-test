pipeline {
  // this is comment
    agent any
    
    stages {
      /*
        stage('Build') {
            steps {
                sh '''
                  ls -la
                  node --version
                  npm --version
                  npm ci
                  npm run build
                  ls -la
                '''
            }
        }
        stage('Test') {
          steps {
            echo 'Test stage'
            sh '''
              test -f build/index.html
              npm test
            '''
          }
        }
        */
        stage('E2E') {
          agent {
            docker {
              image 'mcr.microsoft.com/playwright:v1.61.0-noble'
              reuseNode true
            }
          }
          steps {
            echo 'E2E stage'
            sh '''
              npm ci
              npm run serve:build
              npx playwright test
            '''
          }
        }
    }

    post {
      always {
        junit 'test-results/junit.xml'
      }
    }
}