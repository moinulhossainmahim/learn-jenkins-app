pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '0dd56c9d-e2e3-41a1-a6e0-9806d9b76a99'
    }

    stages {
        stage('build') {
            agent {
                docker {
                    image 'node:22.14-alpine'
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
        stage('test') {
            agent {
                docker {
                    image 'node:22.14-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
        stage('deploy') {
            agent {
                docker {
                    image 'node:22.14-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "Deploying to production. Site ID: $NETLIFY_SITE_ID"
                '''
            }
        }
    }
}
