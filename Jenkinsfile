pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/bmalankou0043-spec/tp-jenkins-security.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                export HOME=/tmp
                python3 -m pip install --upgrade pip
                python3 -m pip install --upgrade wheel
                python3 -m pip install -r requirements.txt
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
                sh '''
                pip install safety
                safety check
                '''
            }
        }

        stage('Static Code Security Scan') {
            steps {
                sh '''
                pip install bandit
                bandit -r .
                '''
            }
        }
        stage('Docker Security Scan') {
    steps {
        sh '''
        docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
        aquasec/trivy image flask-secure-app
        '''
    }
}

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-secure-app .'
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }

        failure {
            echo 'Pipeline failed'
        }
    }
}
