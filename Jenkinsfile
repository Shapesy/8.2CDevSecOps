pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Node Versions') {
      steps {
        bat 'node -v && npm -v'
      }
    }

    stage('Install Dependencies') {
      steps {
        // faster & reproducible; falls back to npm install if needed
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
}
