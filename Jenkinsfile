pipeline {
    agent any
    tools { go 'go-1.19' }
    environment {
        ENV = "${env.BRANCH_NAME == 'master' ? 'PROD' : 'DEV'}"
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'bash scripts/build.sh'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'bash scripts/test.sh'
                }
            }
        }
    }
}