pipeline {
    agent {
        docker {
            image 'python:3.10'
            args '-u root'
        }
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh '''
                python -m pip install --upgrade pip
                pip install -r requirements.txt
                pip install pytest safety bandit
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Dependency Security Scan (SCA)') {
            steps {
                sh 'safety check || true'
            }
        }

        stage('Static Code Security Scan') {
            steps {
                sh 'bandit -r . || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t tp-jenkins-app .'
            }
        }

        stage('Docker Security Scan') {
            steps {
                sh 'docker run --rm aquasec/trivy image tp-jenkins-app || true'
            }
        }

    }

    post {
        success {
            echo 'Pipeline executed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
