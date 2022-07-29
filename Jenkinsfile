pipeline {
    agent any

    stages {
        parallel(
            stage('Build') {
                steps {
                    echo 'Building..'
                }
            }
            stage('Test') {
                steps {
                    echo 'Testing..'
                }
            }
            stage('Deploy') {
                steps {
                    sh echo 'Deploying....'
                    sh echo ${USER_ACCOUNT}
                }
            }
        )
        stage('Docker run') {
            steps {
                sh docker run --rm hello-world
            }
        }
    }
}