pipeline {
    agent any

    triggers {
        // Poll the repo every 5 minutes; githubPush() fires instantly if a webhook is set up
        pollSCM('H/5 * * * *')
        githubPush()
    }

    environment {
        PYTHON = 'C:\Users\jaini\AppData\Local\Programs\Python\Python312\python.exe'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install') {
            steps {
                bat '"%PYTHON%" -m pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                bat '"%PYTHON%" -m pytest --junitxml=report.xml'
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true, testResults: 'report.xml'
        }
    }
}
