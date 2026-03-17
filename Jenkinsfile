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
                pip install safety bandit pytest
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

    }

    post {
        failure {
            echo 'Pipeline failed'
        }
        success {
            echo 'Pipeline succeeded'
        }
    }
}pipeline {
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
                pip install safety bandit pytest
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

    }

    post {
        failure {
            echo 'Pipeline failed'
        }
        success {
            echo 'Pipeline succeeded'
        }
    }
}
