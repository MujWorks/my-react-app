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
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                // SSH to the DigitalOcean CentOS 7 droplet 
                ssh(credentialsId: 'react-key', host: '46.101.84.83', port: 22) {
                    // Create a directory for the React app
                    sh 'sudo mkdir -p /var/www/my-react-app'
                    // Copy the built React app files to the droplet
                    scp src='$WORKSPACE/build', dest='/var/www/my-react-app'
                    // Start the React app
                    sh 'sudo systemctl restart nginx'
                }
            }
        }
    }
}