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
            def timestamp = new Date().format('yyyyMMdd')
            sh "mkdir -p /home/ubuntu/folder-1"
            sh "zip -r /home/ubuntu/folder-1/code-${timestamp}.zip ./Jenkinsfile ./README.md"
            sh "cp /home/ubuntu/folder-1/code-${timestamp}.zip /var/www/html/"
        }
    }
}

        
        stage('Unzip') {
            steps {
                sh "unzip /html/code-${timestamp}.zip -d /var/www/html/"
            }
        }
        
       
    }
}
