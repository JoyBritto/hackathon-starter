pipeline {
  agent any 
     stages {
    stage('Checkout') {
      steps {
        sh 'echo passed'
        //git branch: 'master', url: 'https://github.com/JoyBritto/hackathon-starter.git'
      }
    }
    stage('Test') {
      steps {
        sh 'npm install'  
      }
    }
    stage('Build') {
      steps {
        sh 'npm run build'  
      }
    }
  }
}
