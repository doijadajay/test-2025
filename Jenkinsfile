pipeline {
    agent any

    stages {
        stage('Prepare /mnt/project') {
            steps {
                sh '''
                # Create folder if it doesn't exist
                mkdir -p /mnt/project
                '''
            }
        }

        stage('Clone or Update Repository') {
            steps {
                sh '''
                if [ -d /mnt/project/.git ]; then
                    # Repo already exists, reset and pull latest
                    cd /mnt/project
                    git reset --hard
                    git clean -fd
                    git pull origin main
                else
                    # Clone fresh
                    git clone -b main https://github.com/doijadajay/test-2025.git /mnt/project
                fi
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
