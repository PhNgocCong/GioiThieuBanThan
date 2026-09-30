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
                    npx vercel@latest deploy . \
                      --prod \
                      --token "$VERCEL_TOKEN" \
                      --scope ngoc-cong \
                      --yes
                '''
            }
        }
    }

    post {
        success {
            echo '================================'
            echo '      DEPLOY SUCCESS'
            echo '================================'
            echo 'Website deployed successfully!'
            echo 'https://gioi-thieu-ban-than-six.vercel.app'
        }

        failure {
            echo '================================'
            echo '       DEPLOY FAILED'
            echo '================================'
            echo 'Please check the Console Output.'
        }
    }
}