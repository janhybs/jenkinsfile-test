pipeline {
    agent ci2runner

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                checkout scm
                sh 'ls -la'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'pwd'
                sh 'whoami'
                sh 'echo aaa'
            }
        }
    }
}
