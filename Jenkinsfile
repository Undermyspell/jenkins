pipeline {
    agent any

    stages {
        stage("Parallel") {
            parallel {
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
                        sh "echo Deploying...."
                        sh "echo ${USER_ACCOUNT}"
                        sh "echo Deploy finished..."
                    }
                }
            }
        }
        stage('Docker run') {
            steps {
                sh "docker run --rm hello-world"
            }
        }
    }
}