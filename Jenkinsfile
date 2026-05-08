pipeline {
    agent any
    environment {
        NPM_CONFIG_CACHE = "${WORKSPACE}/.npm"
    }
    stages {
        stage('Buils') {
            agent {
                docker {
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
        stage('TEST') {
              agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            steps {
                sh '''
                echo "Test stage"
                test -f ./build/index.html && echo "File exists" || echo "File not found"
                npm test 
                '''
            }
        }
    }
}
