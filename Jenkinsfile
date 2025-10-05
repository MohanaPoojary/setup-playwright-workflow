pipeline {
    agent any

    tools {
        nodejs 'node-lts' // The name you configured in Jenkins Tools
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone your GitHub repo
                git branch: 'main', url: 'https://github.com/MohanaPoojary/setup-playwright-workflow'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Install Playwright Browsers') {
            steps {
                sh 'npx playwright install --with-deps'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                sh 'npx playwright test'
            }
        }

        stage('Publish Report') {
            steps {
                // Publish HTML report in Jenkins UI
                publishHTML(target: [
                    reportDir: 'playwright-report',
                    reportFiles: 'index.html',
                    reportName: 'Playwright Report'
                ])
            }
        }
    }

    post {
        always {
            // Archive report as a downloadable artifact
            archiveArtifacts artifacts: 'playwright-report/**', fingerprint: true
        }
    }
}
