pipeline {
    agent any

    stages {
        stage('build') {
            agent{
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
            stage('Test') {
                steps{
                    sh '''
                    Test -f build/index.html
                    npm test
                    '''
                }
            }
        }
    }

    post{
        always {
            junit 'test-result/junit.xml'
        }
    }
}
