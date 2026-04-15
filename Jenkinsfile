pipeline {
    agent any
    tools { go 'go-1.19' }
    environment {
        ENV = "${env.BRANCH_NAME == 'main' ? 'PROD' : 'DEV'}"
        BRANCH = "${env.BRANCH_NAME}"
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
        stage('Deploy') {
            when {
                anyOf {
                    branch 'main';
                    branch 'develop'
                }
            }
            steps {
                script {
                    sh 'export JENKINS_NODE_COOKIE=do_not_kill ; bash scripts/deploy.sh'
                }
            }
        }
    }
}