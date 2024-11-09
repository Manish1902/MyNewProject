pipeline {
    agent any

    environment {
        NODE_VERSION = '14' // Specify Node version if need
    }

    tools {
        nodejs "${NODE_VERSION}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from Git
                git branch: 'test', url: 'https://github.com/Manish1902/MyNewProject.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node dependencies
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                // Run build command for web (you can customize for Android or iOS if needed)
                sh 'npx expo build:web'
            }
        }

        stage('Test') {
            steps {
                // Run tests with Jest and output results in JUnit format
                sh 'npm test -- --ci --reporters=jest-junit'
            }
            post {
                always {
                    junit 'jest-junit.xml' // Replace with actual Jest output path
                }
            }
        }

        stage('Security Scan') {
            steps {
                // Placeholder for security testing
                echo 'Running security scans...'
                // Add actual security scan commands or API calls here
            }
        }

        stage('Deploy') {
            steps {
                // Deploy built artifacts to development environment
                echo 'Deploying to server...'
                // Commands for deployment to your environment
            }
        }
    }

    post {
        failure {
            echo 'Build failed!'
            mail to: 'your-email@example.com',
                 subject: "Jenkins Pipeline Failed: ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                 body: "Something is wrong with ${env.JOB_NAME}. Please check console output."
        }
    }
}