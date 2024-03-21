pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                // GitHub deposunu klonla
                git 'https://github.com/nvnsrky/hello-world-NGINX.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Dockerfile'ı kullanarak Docker imajını oluştur
                script {
                    dockerImage = docker.build("hello-world-nginx:${env.BUILD_ID}")
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                // Docker konteynerını çalıştır
                script {
                    dockerImage.run("-p 8080:80 -d")
                }
            }
        }
    }
    
    post {
        always {
            // Her durumda Docker konteynerını durdur ve temizle
            cleanWs()
            script {
                dockerImage.stop()
                dockerImage.remove()
            }
        }
    }
}
