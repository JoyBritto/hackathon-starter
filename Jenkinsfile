pipeline {
    agent any

    environment {
        NODE_VERSION = '14' // Adjust to your Node.js version
        KUBE_NAMESPACE = 'App'
        KUBE_DEPLOYMENT_NAME = 'Node JS'
        KUBE_CONTAINER_NAME = 'your_container_name'
        KUBE_CLUSTER = 'your_kube_cluster'
        KUBE_SERVER = 'your_kube_server'
        KUBE_CREDENTIALS = credentials('your_kube_credentials_id')
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

        stage('Scan Images for Vulnerabilities') {
            steps {
                script {
                    // Use Trivy to scan the container image for vulnerabilities
                    def trivyResult = sh(script: 'trivy -q --severity HIGH,CRITICAL -f json .', returnStatus: true)

                    if (trivyResult == 0) {
                        echo "No HIGH or CRITICAL vulnerabilities found."
                    } else {
                        error "Aborting build due to HIGH or CRITICAL vulnerabilities detected."
                    }
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('YourSonarQubeServer') {
                        // Run SonarQube analysis
                        sh 'npm install -g sonarqube-scanner'
                        sh 'sonar-scanner -Dsonar.login=admin -Dsonar.password=admin -Dsonar.projectKey=your_project_key -Dsonar.projectName=sonarqube'
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Authenticate with Kubernetes
                    withCredentials([[$class: 'KubeconfigContentBinding', credentialsId: env.KUBE_CREDENTIALS, kubeconfigContent: env.KUBE_CONFIG]]) {
                        // Deploy to Kubernetes
                        sh "kubectl config use-context ${env.KUBE_CLUSTER}"
                        sh "kubectl set image deployment/${env.KUBE_DEPLOYMENT_NAME} ${env.KUBE_CONTAINER_NAME}=your_registry/your_image:your_tag -n ${env.KUBE_NAMESPACE}"
                    }
                }
            }
        }
