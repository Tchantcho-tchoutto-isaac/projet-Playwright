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
                 echo "🚀 Exécution des tests Playwright avec génération de rapport JUnit..."
                sh 'npx playwright test --reporter=junit,junit-output=test-results/results.xml'
            }
        }

        stage('Publish Test Report') {
            steps {
                 echo "📊 Publication du rapport JUnit sur Jenkins..."
                junit 'test-results/results.xml'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
