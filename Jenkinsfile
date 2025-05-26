pipeline {
    agent any
    stages {
    
        stage('Checkout') {
            steps {
                git 'https://github.com/adityasubhash35/8.2DevSecOps.git'
            }
        }
        

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit'
            }
        }
    }
}
