pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            reuseNode true
                }
        }

    environment{
        NETLIFY_SITE_ID = 'b87eb8f4-7e2b-41d5-b25e-c7c949e99e07'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
    }

    stages {

        stage('Build') {
            
            
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }


        stage('Deploy') {
            
            steps {
                sh '''
                    ls -la
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "deploying to production site id :$NETLIFY_SITE_ID"
                    node_modules/.bin/netlify status
                    node_modules/.bin/netlify deploy --dir=build --prod
                '''
            }
        }
    }
}
