pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    // Di chuyển đến thư mục dự án
                    dir('/home/hongdatchy/simple_spring') {
                        // Build project bằng Maven
                        sh 'git pull origin master'
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
                        // Chạy ứng dụng Spring Boot
                        sh "pid=\$(lsof -i:8081 -t); kill -TERM \$pid "
                                          + "|| kill -KILL \$pid"
                        withEnv(['JENKINS_NODE_COOKIE=dontkill']) {
                            sh 'nohup ./mvnw spring-boot:run -Dserver.port=8081 &'
                        }
                    }
                }
            }
        }

    }
}
