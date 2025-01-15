pipeline {
    agent any

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
    }
}
