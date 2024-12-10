pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Kuraye/PythonPipeline.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Assuming Python and pip are installed
                    sh 'python -m venv venv'
                    sh 'source venv/bin/activate'
                    sh 'pip install -r requirements.txt'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'python -m venv venv'
                    sh 'source venv/bin/activate'
                    sh 'pip install -r requirements.txt'
                    sh 'pytest'
                }
            }
        }
        stage('Deploy') {
            when {
                expression { env.BRANCH_NAME == 'main' }
            }
            steps {
                script {
                    echo 'Deploying...'
                }
            }
        }
    }
}
