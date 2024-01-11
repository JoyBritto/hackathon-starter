pipeline {
    agent any

    environment {
        // Define environment variables if needed
        NODE_VERSION = '14' // Adjust to your Node.js version
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Environment') {
            steps {
                script {
                    // Use Node.js tool installer to ensure the correct Node version
                    def nodeHome = tool 'NodeJS_' + env.NODE_VERSION
                    env.PATH = "${nodeHome}/bin:${env.PATH}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'npm test'
                }
            }
        }
    }
}
