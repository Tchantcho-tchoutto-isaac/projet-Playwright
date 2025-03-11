pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.50.0-noble'
            args '--user root'
        }
    }

    stages {

        stage('Run Playwright Tests') {
            steps {
                echo "🚀 Exécution des tests Playwright..."
                sh 'npx playwright test'
            }
        }

        stage('Publish Test Report') {
            steps {
                sh 'npx playwright show-report'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
