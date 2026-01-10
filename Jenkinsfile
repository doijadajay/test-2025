pipeline {
    agent any

    stages {
        stage('Prepare /mnt/project') {
            steps {
                sh '''
                # Create /mnt/project if it doesn't exist
                mkdir -p /mnt/project

                # Clean only /mnt/project, not /mnt root
                rm -rf /mnt/project/*
                '''
            }
        }

        stage('Clone Repository') {
            steps {
                sh '''
                # Clone the public repo directly into /mnt/project
                git clone -b main https://github.com/doijadajay/test-2025.git /mnt/project
                '''
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                # Copy index.html to Apache web root
                cp /mnt/project/index.html /var/www/html/

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
            echo '❌ Deployment failed! Check the console output.'
        }
    }
}
