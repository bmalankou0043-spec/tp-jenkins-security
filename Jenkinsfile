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
     safety check -r requirements.txt
        pip install bandit safety pytest
        '''
    }
}

        stage('Run Tests') {
            steps {
                sh '''
                pip install pytest
                pytest
                '''
            }
        }

 stage('Dependency Security Scan (SCA)') {
    steps {
        sh 'safety check -r requirements.txt'
    }
}
        stage('Static Code Security Scan') {
    steps {
        sh 'bandit -r .'
    }
}

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t jenkins-secure-app .
                '''
            }
        }

        stage('Docker Security Scan') {
            steps {
                sh '''
                docker run --rm aquasec/trivy image jenkins-secure-app
                '''
            }
        }

    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
