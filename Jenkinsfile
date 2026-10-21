pipeline {
    agent any

    triggers {
        // Fires when GitHub sends a push webhook to <jenkins>/github-webhook/
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install') {
            steps {
                dir('p9') {
                    bat 'python -m pip install -r requirements.txt'
                }
            }
        }
        stage('Test') {
            steps {
                dir('p9') {
                    bat 'python -m pytest --junitxml=report.xml'
                }
            }
        }
    }

    post {
        always {
            junit 'p9/report.xml'
        }
    }
}
