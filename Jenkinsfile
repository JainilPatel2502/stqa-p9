pipeline {
    agent any

    triggers {
        // Poll the repo every 5 minutes; githubPush() fires instantly if a webhook is set up
        pollSCM('H/5 * * * *')
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
                bat 'python -m pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                bat 'python -m pytest --junitxml=report.xml'
            }
        }
    }

    post {
        always {
            junit 'report.xml'
        }
    }
}
