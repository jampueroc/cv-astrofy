pipeline {
    agent {
        node {
            label 'node-cv' // Ajusta el label si es necesario
        }
    }

    environment {
        DEPLOY_PATH = '/var/www/ampuero.me'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    sh """
                    cd website
                    CURRENT_BRANCH=\$(git rev-parse --abbrev-ref HEAD)
                    if [ "\$CURRENT_BRANCH" != "main" ]; then
                        git checkout main
                    fi
                    git pull origin main
                    """
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'cd website && npm ci'
            }
        }

        stage('Build Astro') {
            steps {
                sh 'cd website && npm run build'
            }
        }

        stage('Copy to /var/www/ampuero.me') {
            steps {
                script {
                    sh """
                    sudo rm -rf ${DEPLOY_PATH}/*
                    sudo cp -r website/dist/* ${DEPLOY_PATH}/
                    """
                }
            }
        }

        stage('Clean Build') {
            steps {
                sh 'rm -rf website/dist'
            }
        }
    }
}