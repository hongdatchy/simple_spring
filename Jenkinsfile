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
                    PID=$(lsof -t -i:8081)
                    if [ -n "$PID" ]; then
                      echo "Stopping process with PID: $PID"
                      kill -9 $PID
                    else
                      echo "No process is running on port 8081"
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
