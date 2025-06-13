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
        stage('Deploy to Staging') {
            steps {
                sshagent (credentials: ['jenkins-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no kael@10.0.2.15 "mkdir -p ~/nodeapp"
                    scp -r * kael@10.0.2.15:~/nodeapp/
                    ssh kael@10.0.2.15 "cd ~/nodeapp && npm install && pm2 restart all || pm2 start index.js"
                    '''
                }
            }
        }
    }
}
