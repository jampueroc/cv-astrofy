pipeline {
    agent {
        node {
            label 'node-cv' // Ajusta el label si es necesario
        }
    }

    environment {
        DEPLOY_USER = 'jorge'
        DEPLOY_HOST = 'ampuero.me'
        DEPLOY_PATH = '/var/www/ampuero.me'
        SSH_KEY = credentials('jenkins-ssh-key') // Asegúrate de que Jenkins tenga una credencial SSH configurada
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:tu-repo/tu-proyecto.git' // Cambia por tu repositorio
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

        stage('Deploy via SCP') {
            steps {
                script {
                    // Usamos SCP para transferir los archivos compilados
                    sh """
                    ssh -i ${SSH_KEY} ${DEPLOY_USER}@${DEPLOY_HOST} "rm -rf ${DEPLOY_PATH}/*"
                    scp -i ${SSH_KEY} -r ./dist/* ${DEPLOY_USER}@${DEPLOY_HOST}:${DEPLOY_PATH}
                    """
                }
            }
        }
    }
}