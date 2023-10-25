pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MujWorks/my-react-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'nvm install 14'  // Use a compatible Node.js version
                sh 'nvm use 14'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'npm run build'
                // You can deploy to a server or cloud platform here
                // For simplicity, we're not covering deployment in this example.
            }
        }
    }
}
