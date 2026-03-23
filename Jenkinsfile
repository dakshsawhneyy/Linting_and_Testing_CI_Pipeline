pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/dakshsawhneyy/Linting_and_Testing_CI_Pipeline.git', branch: 'master'
            }
        }
        stage('Build') {
            steps {
                echo 'Building Application'
            }
        }
        stage('Install pip') {
            steps {
                sh '''
                    curl -sS https://bootstrap.pypa.io/get-pip.py -o get-pip.py
                    python3 get-pip.py --break-system-packages
                '''
            }
        }
        stage('Installing Dependencies') {
            steps {
                sh '''
                    python3 -m pip install -r requirements.txt --break-system-packages
                '''
            }
        }
        stage('Lint'){
            steps{
                sh 'python3 -m flake8 . --exclude=get-pip.py,__pycache__,.git'
            }
        }
        stage('Testing') {
            steps {
                sh 'python3 test_app.py'
            }
        }
    }

    post {
        success {
            echo "Build Successful"
        }
        failure {
            echo "Build Failed"
        }
    }
}
