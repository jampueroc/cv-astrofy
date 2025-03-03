pipeline {
  agent {
    node {
      label 'node-cv'
    }

  }
  stages {
    stage('Build') {
      steps {
        node(label: '001') {
          build 'build'
          sh 'npm ci && npm build'
        }

      }
    }

  }
}