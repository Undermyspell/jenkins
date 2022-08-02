def getDockerTag() {
    def today = new Date() 
    return today.format("yyyy.MM.dd:") + "${GIT_COMMIT}"[0..7]
}

pipeline {
    agent any
    environment {
        DOCKER_TAG = getDockerTag()
    }
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
        stage("Parallel2") {
            steps {
                echo "Going parallel"
            }
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
        stage('Print Build Tag') {
            steps {
                sh "echo ${GIT_COMMIT}"
                sh "echo ${DOCKER_TAG}"
            }
        }
        stage('Docker build') {
            steps {
                sh "docker build -t ng-sample ./ng-sample"
            }
        }
         stage('Docker clean') {
            steps {
                sh "docker rmi -f ng-sample"
            }
        }
    }
}