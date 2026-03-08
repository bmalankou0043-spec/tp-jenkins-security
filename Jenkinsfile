pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/bmalankou0043-spec/tp-jenkins-security.git'
            }
        }

        stage('Install Python') {
            steps {
                sh 'apt-get update'
                sh 'apt-get install -y python3 python3-pip'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('SCA Scan') {
            steps {
                sh 'echo "OWASP Dependency Check simulation"'
            }
        }
    }

    post {
        failure {
            echo 'Build failed due to errors or vulnerabilities'
        }
    }
}
