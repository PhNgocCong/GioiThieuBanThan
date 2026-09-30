pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('vercel-token')
    }

    stages {

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

        stage('Check Node.js') {
            steps {
                echo '===== CHECK NODE.JS ====='

                sh '''
                    echo "Node.js:"
                    node -v

                    echo "npm:"
                    npm -v

                    echo "npx:"
                    npx --version
                '''
            }
        }

        stage('Check Vercel Token') {
            steps {
                echo '===== CHECK VERCEL TOKEN ====='

                sh '''
                    if [ -z "$VERCEL_TOKEN" ]; then
                        echo "ERROR: VERCEL_TOKEN is empty"
                        exit 1
                    fi

                    echo "Vercel token is available"
                    echo "Token length: ${#VERCEL_TOKEN}"
                '''
            }
        }

        stage('Deploy to Vercel') {
            steps {
                echo '===== DEPLOY TO VERCEL ====='

                sh '''
                    npx vercel deploy \
                        --prod \
                        --token "$VERCEL_TOKEN" \
                        --yes
                '''
            }
        }
    }

    post {
        success {
            echo '===================================='
            echo '       DEPLOY SUCCESS'
            echo '===================================='
            echo 'Website deployed successfully!'
        }

        failure {
            echo '===================================='
            echo '       DEPLOY FAILED'
            echo '===================================='
            echo 'Please check the failed stage above.'
        }
    }
}