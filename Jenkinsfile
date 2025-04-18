pipeline {
    agent any

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
    }
}
