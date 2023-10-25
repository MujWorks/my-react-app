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
                script {
                    // SSH to the DigitalOcean CentOS 7 droplet    
                    sshCommand remote: [credentialsId: 'react-key', name: '46.101.84.83'], command: '''
                        # Create a directory for the React app (if it doesn't exist)
                        sudo mkdir -p /usr/share/nginx/html/my-react-app
                        # Copy the built React app files to the server root directory
                        sudo cp -r $WORKSPACE/build/* /usr/share/nginx/html/my-react-app/
                        # Restart the Nginx web server
                        sudo systemctl restart nginx
                    '''
                }
            }
        }
    }
}
