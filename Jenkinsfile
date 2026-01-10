pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Use a dedicated folder inside /mnt for Jenkins
                sh '''
                mkdir -p /mnt/jenkins_builds/test-2025
                rm -rf /mnt/jenkins_builds/test-2025/*
                git clone -b main https://github.com/doijadajay/test-2025.git /mnt/jenkins_builds/test-2025
                '''
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                # Copy index.html from the dedicated build folder to Apache web root
                cp /mnt/jenkins_builds/test-2025/index.html /var/www/html/
                
                # Restart Apache safely
                systemctl restart httpd || systemctl restart apache2
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment completed successfully!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
