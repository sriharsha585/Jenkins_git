pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sriharsha585/Jenkins_git.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'   // or npm install, etc.
            }
        }
        stage('Deploy') {
    steps {
        sshagent(['ec2-key']) {
            sh 'scp -o StrictHostKeyChecking=no target/app.jar ec2-user@3.87.237.90:/home/ec2-user/'
            sh 'ssh -o StrictHostKeyChecking=no ec2-user@3.87.237.90 "nohup java -jar /home/ec2-user/app.jar > app.log 2>&1 &"'
        }
    }
}
}