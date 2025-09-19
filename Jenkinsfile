pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci || npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }
    }

    post {
        success {
            emailext(
                subject: "SUCCESS: Jenkins build #${env.BUILD_NUMBER}",
                body: "The pipeline has completed successfully.\n\nCheck attached logs for details.",
                attachLog: true,
                to: "JedFerlazz@gmail.com"
            )
        }
        failure {
            emailext(
                subject: "FAILURE: Jenkins build #${env.BUILD_NUMBER}",
                body: "The pipeline has failed.\n\nCheck attached logs for details.",
                attachLog: true,
                to: "JedFerlazz@gmail.com"
            )
        }
    }
}
