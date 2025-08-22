pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Avanish-Iyengar/exp3.git'
            }
        }

        stage('Set up Python') {
            steps {
                // Create virtual environment and install dependencies
                sh '''
                    python3 -m venv venv
                    source venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    source venv/bin/activate
                    pytest --maxfail=1 --disable-warnings -q
                '''
            }
        }

        stage('Lint') {
            steps {
                sh '''
                    source venv/bin/activate
                    pip install flake8
                    flake8 .
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment step (e.g. upload to server, dockerize, etc.)'
            }
        }
    }

    post {
        always {
            junit 'tests/**/*.xml'   // if pytest is configured to generate JUnit XML
            echo 'Pipeline finished.'
        }
    }
}
