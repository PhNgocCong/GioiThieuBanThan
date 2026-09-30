pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('vercel-token')
    }

    stages {

        stage('Checkout') {
            steps {
                echo '===== CHECKOUT GITHUB ====='
                checkout scm
            }
        }

        stage('Check Website') {
            steps {
                echo '===== CHECK WEBSITE ====='

                bat '''
                    if not exist index.html (
                        echo ERROR: index.html not found
                        exit /b 1
                    )

                    echo index.html found successfully
                '''
            }
        }

        stage('Deploy to Vercel') {
            steps {
                echo '===== DEPLOY TO VERCEL ====='

                bat '''
                    npx vercel deploy --prod --token "%VERCEL_TOKEN%" --yes
                '''
            }
        }
    }

    post {
        success {
            echo '===== DEPLOY SUCCESS ====='
            echo 'Website deployed successfully!'
        }

        failure {
            echo '===== DEPLOY FAILED ====='
            echo 'Please check Jenkins Console Output.'
        }
    }
}