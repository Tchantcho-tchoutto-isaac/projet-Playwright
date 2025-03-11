pipeline {
    environment {
        DOCKER_HOST = "tcp://localhost:2375"
    }

    agent any

    stages {
        stage('Test Docker Connection') {
            steps {
                script {
                    def dockerHost = sh(script: 'echo $DOCKER_HOST', returnStdout: true).trim()
                    echo "DOCKER_HOST from Jenkins: ${dockerHost}"
                }
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
