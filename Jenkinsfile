pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID = 'a75245a9-7ac6-4638-a477-6f701cd55381'
    }

    stages {
        
        stage('Build'){
            agent{
                docker{
                    image "node:23-alpine"
                    reuseNode true
                }
            }
            steps{
                // ceci pour tracer lors des nouveaux build pour voir ci on a zaper la version node
                // npm ci --> clean install for ci / cd measures
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
        
        stage('Test'){

            agent{
                docker{
                    image 'node:23-alpine'
                    reuseNode true
                }
            }

            steps{
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }

        stage('Deploy'){

            agent{
                docker{
                    image 'node:23-alpine'
                    reuseNode true
                }
            }

            steps{
                // installing netlify creates permission errors and so we install it and 
                // call it from the node-modules folder
                sh '''
                    ls -la
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "deploying to production site ID: $NETLIFY_SITE_ID"
                '''
            }
        }
    }

    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}

