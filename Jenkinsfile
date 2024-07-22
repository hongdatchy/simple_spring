pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    // Di chuyển đến thư mục dự án
                    dir('/home/hongdatchy/simple_spring') {
                        // Pull latest code from git
                        sh 'git pull origin master'
                        // Build project using Maven
                        sh 'mvn clean install'
                    }
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    // Di chuyển đến thư mục dự án
                    dir('/home/hongdatchy/simple_spring') {
                        // Chạy ứng dụng Spring Boot trong nền
                        sh 'mvn spring-boot:start'
                    }
                }
            }
        }
    }
    post {
        always {
            script {
                // Dừng ứng dụng Spring Boot
                dir('/home/hongdatchy/simple_spring') {
                    sh 'mvn spring-boot:stop'
                }
            }
        }
    }
}
