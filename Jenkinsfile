pipeline {
  agent any 
     stages {
    stage('Checkout') {
      steps {
        sh 'echo passed'
        //git branch: 'master', url: 'https://github.com/JoyBritto/hackathon-starter.git'
      }
    }
    stage('Build and Test') {
      steps {
        sh 'npm install'  
      }
    }
