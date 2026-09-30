pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('vercel-token')
        VERCEL_ORG_ID = 'team_wkzwr9dUQiqed0JN8e8Iul4s'
        VERCEL_PROJECT_ID = 'prj_LyOD4Ks52FnImUfN2ZSGIPO9rlUp'
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
                    node -v
                    npm -v
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

                    echo "Vercel token exists"
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
                        --yes \
                        --scope ngoc-cong \
                        --project "$VERCEL_PROJECT_ID"
                '''
            }
        }
    }

    post {
        success {
            echo '===================================='
            echo '       DEPLOY SUCCESS'
            echo '===================================='
            echo 'Website: https://gioi-thieu-ban-than-six.vercel.app'
        }

        failure {
            echo '===================================='
            echo '       DEPLOY FAILED'
            echo '===================================='
            echo 'Please check the Console Output.'
        }
    }
}