pipeline {
    agent any

    stages {
        stage('Prepare /mnt/project') {
            steps {
                sh '''
                mkdir -p /mnt/project
                rm -rf /mnt/project/*
                cp -r $WORKSPACE/* /mnt/project/
                '''
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                cp /mnt/project/index.html /var/www/html/
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
