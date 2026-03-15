pipeline {
    agent {
        docker {
            image 'python:3.10'
        }
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/bmalankou0043-spec/tp-jenkins-security.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('SCA Scan') {
            steps {
                sh '''
                pip install safety
                safety check
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully'
        }
        failure {
            echo 'Build failed due to errors or vulnerabilities'
        }
    }
}
