pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/2017ugec/demo_pipeline'
      }
    }
    
    stage('Build') {
      steps {
        script {
          docker.build('my-pandas-app:latest', '-f Dockerfile .')
        }
      }
    }
    
    stage('Test') {
      steps {
        script {
          docker.image('my-pandas-app:latest').run('--name my-pandas-container')
          docker.cp('my-pandas-container:/app/output.txt', '.')
          docker.stop('my-pandas-container')
          docker.rm('my-pandas-container')
        }
      }
    }
    
    stage('Publish') {
      steps {
        script {
          archiveArtifacts artifacts: 'output.txt', onlyIfSuccessful: false
        }
      }
    }
  }
}
