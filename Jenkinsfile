pipeline {
    agent any
    
    environment {
        // Define environment variables here        
        // REMOTE_SERVER = '209.97.134.94'
        REMOTE_SERVER = '10.106.0.2'
        REMOTE_USER = 'root'
        REMOTE_PORT = '22' // Default SSH port
        //PROJECT_DIR = '/usr/share/nginx/html/my-react-app' // Remote directory where your project should be deployed
        PROJECT_DIR = '/var/www/html' // Remote directory where your project should be deployed
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your GitHub repository
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanBeforeCheckout']], userRemoteConfigs: [[url: 'https://github.com/MujWorks/my-react-app.git']]])
            }
        }

        stage('Build') {
            steps {
                // Install dependencies and build the React app
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Copy the built project to the Nginx server using SSH                      
                script {
                    sshagent(['MySSHKey']) {
                        //sh "scp -r -P ${REMOTE_PORT} build/* ${REMOTE_USER}@${REMOTE_SERVER}:${PROJECT_DIR}"

                        //detailed debugging
                        // ssh -o StrictHostKeyChecking=no -p ${REMOTE_PORT} ${REMOTE_USER}@${REMOTE_SERVER} 'mkdir -p ${PROJECT_DIR}'                        
                        sh """
                        set -x
                        ssh -o StrictHostKeyChecking=no -p ${REMOTE_PORT} ${REMOTE_USER}@${REMOTE_SERVER} 'mkdir -p ${PROJECT_DIR}'
                        scp -r -P ${REMOTE_PORT} build/* ${REMOTE_USER}@${REMOTE_SERVER}:${PROJECT_DIR}
                        """
                    }
                }
            }
        }

        // stage('Deploy') {
        //     steps {
        //         // Copy the built project to the Nginx server using SSH    
        //         sh "ssh -o StrictHostKeyChecking=no -p ${REMOTE_PORT} ${REMOTE_USER}@${REMOTE_SERVER} 'mkdir -p ${PROJECT_DIR}'"
        //         sh "scp -o StrictHostKeyChecking=no -r -P ${REMOTE_PORT} build/* ${REMOTE_USER}@${REMOTE_SERVER}:${PROJECT_DIR}"
        //     }
        // }
    }
}
