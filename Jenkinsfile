pipeline {
    agent any

    stages {
        stage('without docker') {
            steps {
                echo 'Hello World'
                sh '''
                    echo "Without docker"
                    ls -la
                '''
            }
        }
        // stage('with docker') {
        //     agent{
        //         docker{
        //             image 'node:18-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         echo 'Hello World'
        //         sh '''
        //             echo "With docker"
        //             ls -la
        //             touch container-yes.txt
        //         '''
        //     }
        // }
    }
}
