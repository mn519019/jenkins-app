pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = '4dd0a065-f618-4a7b-b021-4a1b6dd459e9'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }

    stages {
        // stage('without docker') {
        //     steps {
        //         echo 'Hello World'
        //         sh '''
        //             echo "Without docker"
        //             ls -la
        //         '''
        //     }
        // }
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Hello World'
                sh '''
                    ls -la
                    echo "Node & NPM Version"
                    node --version
                    npm --version
                    npm ci
                    echo "Starting build..."
                    npm run build
                '''
            }
        }

        stage('Test') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Test stage'
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }

        }

        stage('Deploy') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Hello World'
                sh '''
                    npm install netlify-cli 
                    npm config set strict-ssl false
                    node_modules/.bin/netlify --version
                    echo "Deploying to proudction. Site ID: $NETLIFY_SITE_ID"
                    node_modules/.bin/netlify status
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
