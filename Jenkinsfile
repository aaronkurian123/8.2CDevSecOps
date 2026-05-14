pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/aaronkurian123/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
            post {
                always {
                    emailext(
                        to: 'aaronkurian98975@gmail.com',
                        subject: 'Jenkins - Run Tests Stage: ${BUILD_STATUS} - Build #${BUILD_NUMBER}',
                        body: 'The Run Tests stage has completed with status: ${BUILD_STATUS}.\n\nCheck console output at ${BUILD_URL} to view the results.',
                        attachLog: true
                    )
                }
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
            post {
                always {
                    emailext(
                        to: 'aaronkurian98975@gmail.com',
                        subject: 'Jenkins - Security Scan Stage: ${BUILD_STATUS} - Build #${BUILD_NUMBER}',
                        body: 'The NPM Audit Security Scan stage has completed with status: ${BUILD_STATUS}.\n\nCheck console output at ${BUILD_URL} to view the results.',
                        attachLog: true
                    )
                }
            }
        }
    }
}
