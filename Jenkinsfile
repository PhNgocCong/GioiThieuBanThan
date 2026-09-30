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

                sh '''
                    if [ ! -f index.html ]; then
                        echo "ERROR: index.html not found"
                        exit 1
                    fi

                    echo "index.html found successfully"
                '''
            }
        }

        stage('Check Node') {
            steps {
                echo '===== CHECK NODE.JS ====='

                sh '''
                    node -v
                    npm -v
                    npx --version
                '''
            }
        }

        stage('Deploy to Vercel') {
            steps {
                echo '===== DEPLOY TO VERCEL ====='

                sh '''
                    npx vercel deploy --prod --token "$VERCEL_TOKEN" --yes
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