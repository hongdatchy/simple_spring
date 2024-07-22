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
                        sh "JENKINS_NODE_COOKIE=dontKillMe nohup java -jar target/SimpleSpring-0.0.1-SNAPSHOT.jar > app.log 2>&1 &"
                    }
                }
            }
        }
    }
}
