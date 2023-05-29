pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: 'https://github.com/Meenakshi0812/pipeline-html.git']]])
            }
        }
        
        stage('Create and Copy ZIP') {
            steps {
                script {
                    def timestamp = new Date().format('yyyyMMdd_HHmmss')
                    sh "mkdir -p /home/ubuntu/folder-1"
                    sh "zip -r /home/ubuntu/folder-1/code-${timestamp}.zip ./Jenkinsfile ./README.md"
                    sh "cp /home/ubuntu/folder-1/code-${timestamp}.zip /var/www/html/"
                    
                    // Store the timestamp in an environment variable for later use
                    env.TIMESTAMP = timestamp
                }
            }
        }
        
        stage('Unzip') {
            steps {
                script {
                    // Retrieve the timestamp from the environment variable
                    def timestamp = env.TIMESTAMP
                    sh "unzip /var/www/html/code-${timestamp}.zip -d /var/www/html/"
                }
            }
        }
    }
}
