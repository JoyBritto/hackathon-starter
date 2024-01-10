pipeline {
    agent any
    
    environment {
        // Define environment variables if needed
        NODE_VERSION = '14' // Example Node.js version
    }
    
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: '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', 
                url: 'https://github.com/JoyBritto/hackathon-starter.git',
                branch: 'master'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                // Use Node.js specified in environment to install dependencies
                sh "nvm install ${NODE_VERSION}"
                sh "nvm use ${NODE_VERSION}"
                sh 'npm install'
            }
        }
        
        stage('Run Tests') {
            steps {
                // Run tests if specified in the README or using npm test script
                sh 'npm test'
            }
        }
     }
  }
