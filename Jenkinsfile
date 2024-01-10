pipeline {
    agent any
    
    environment {
        // Define environment variables if needed
        NODE_VERSION = '14' // Example Node.js version
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                git 'https://github.com/JoyBritto/hackathon-starter.git'
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
