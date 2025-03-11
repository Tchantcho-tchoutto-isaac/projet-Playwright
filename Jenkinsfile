pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.50.0-noble'
        }
    }

    stages {
        

        stage('Run Playwright Tests') {
            steps {
                echo "Exécution des tests Playwright..."
                sh 'npx playwright test'
            }
        }

      
    }
}
