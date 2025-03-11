pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.50.0-noble'
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
            
                 sh 'npx playwright test --reporter=line,allure-playwright'
                stash name: 'allure-results', includes: 'allure-results/*'
            }
        }

        stage('Publish Test Report') {
            steps {
                echo "📊 Publication du rapport JUnit sur Jenkins..."
                junit 'test-results/*.xml'
            }
        }
    }

    post {
        always {
            unstash 'allure-results' //extract results
            script {
                allure([
                includeProperties: false,
                jdk: '',
                properties: [],
                reportBuildPolicy: 'ALWAYS',
                results: [[path: 'allure-results']]
            ])
            }
        }
    }
}
