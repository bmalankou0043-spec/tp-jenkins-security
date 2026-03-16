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
        export HOME=/tmp
        python -m pip install --upgrade pip
        python -m pip install --upgrade wheel
        python -m pip install --no-cache-dir -r requirements.txt
        '''
    }
}

        stage('Run Tests') {
            steps {
                sh '''
                export HOME=/tmp
                python -m pytest
                '''
            }
        }

        stage('SCA Scan') {
            steps {
                sh '''
                export HOME=/tmp
                pip install --user safety
                python -m safety check
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
