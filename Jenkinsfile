pipeline {
    agent any

    stages {
        stage('Deploy to Apache') {
            steps {
                sh '''
                # Create a safe build folder inside /mnt (optional)
                mkdir -p /mnt/jenkins_builds/test-2025

                # Copy index.html from Jenkins workspace (already cloned) to Apache web root
                cp $WORKSPACE/index.html /var/www/html/

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
