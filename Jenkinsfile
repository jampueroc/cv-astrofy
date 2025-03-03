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
                git branch: 'main', url: 'git@github.com:jampueroc/cv-astrofy.git' // Cambia por tu repositorio
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Build Astro') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Copy to /var/www/ampuero.me') {
            steps {
                script {
                    sh """
                    sudo rm -rf ${DEPLOY_PATH}/*
                    sudo cp -r ./dist/* ${DEPLOY_PATH}/
                    """
                }
            }
        }

        stage('Clean Build') {
            steps {
                sh 'rm -rf ./dist'
            }
        }
    }
}