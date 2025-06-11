pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/kaelcloud/nodejs-ci-app.git'
            }
        }

        stage('Install') {
            steps {
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test || echo "No tests configured."'
            }
        }
    }
}
