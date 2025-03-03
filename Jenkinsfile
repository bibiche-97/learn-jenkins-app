pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true

                }
            }
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
              agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true

                }
            }
             steps {
                sh '''
                    echo "Testing..."
                    test -f build/index.html
                    npm test
                '''
            }
        }
    }
    post {
        always {
           junit 'test-results/junit.xml'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
    }
}