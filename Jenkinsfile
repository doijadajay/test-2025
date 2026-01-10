pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clone repo into /mnt/test-2025
                sh 'rm -rf /mnt/test-2025'  // clean previous clone
                sh 'git clone -b main https://github.com/doijadajay/test-2025.git /mnt/test-2025'
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                # Copy index.html from /mnt/test-2025 to Apache web root
                cp /mnt/test-2025/index.html /var/www/html/
                
                # Restart Apache
                systemctl restart httpd
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
