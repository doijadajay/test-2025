pipeline {
    agent any

    stages {
        stage('Prepare Build Directory') {
            steps {
                sh '''
                # Create a safe folder for Jenkins builds
                mkdir -p /mnt/jenkins_builds/test-2025
                
                # Clean only the build folder, not /mnt root
                rm -rf /mnt/jenkins_builds/test-2025/*
                '''
            }
        }

        stage('Clone Repository') {
            steps {
                sh '''
                # Clone the public repo into the dedicated build folder
                git clone -b main https://github.com/doijadajay/test-2025.git /mnt/jenkins_builds/test-2025
                '''
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                # Copy index.html to Apache web root
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
            echo '❌ Deployment failed! Check the console output.'
        }
    }
}
