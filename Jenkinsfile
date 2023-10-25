pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MujWorks/my-react-app.git'
            }
        }
        

stage('Configure nvm and Install Node.js') {
    steps {
        sh 'nvm install 14'  // Install Node.js version 14
        sh 'nvm use 14'     // Use Node.js version 14
    }
}

        stage('Build') {
            steps {
                sh 'nvm install 14'  // Use a compatible Node.js version
                sh 'nvm use 14'
                sh 'npm install'
                sh 'npm install typescript@3.2'  // Install the missing TypeScript version
        sh 'npm install ajv@8'  // Install the missing ajv version
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
