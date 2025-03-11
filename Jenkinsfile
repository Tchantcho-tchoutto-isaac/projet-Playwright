pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.50.0-noble'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
       

        stage('Install Dependencies') {
            steps {
                echo "📦 Installation des dépendances..."
                sh 'npm install'
                sh 'npx playwright install'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                echo "🚀 Exécution des tests Playwright..."
                sh 'npx playwright test'
            }
        }

        stage('Publish Test Report') {
            steps {
                echo "📊 Génération du rapport Playwright..."
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
