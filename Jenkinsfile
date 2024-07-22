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
                    sh '''
                    PID=$(lsof -t -i:8080)
                    if [ -n "$PID" ]; then
                      kill -9 $PID
                    fi
                    '''
                    // Di chuyển đến thư mục dự án
                    dir('/home/hongdatchy/simple_spring') {
                        // Chạy ứng dụng Spring Boot trong nền
                        sh 'nohup mvn spring-boot:run &'
                    }
                }
            }
        }
    }
}
