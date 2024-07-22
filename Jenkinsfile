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
                    // Dừng tiến trình Spring Boot cũ nếu có

                    // Di chuyển đến thư mục dự án
                    dir('/home/hongdatchy/simple_spring') {
                        kill -9 $(lsof -t -i:8081) || echo "Process was not running."
                        echo "mvn spring-boot:run" | at now + 1 minutes
                    }
                }
            }
        }
    }
}
