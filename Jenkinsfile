pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/yourusername/my-react-app.git'
            }
        }
        stage('Build') {
            steps {
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
                // For simplicity, we're not covering deployment in this example
            }
        }
    }
}
