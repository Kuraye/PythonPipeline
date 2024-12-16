pipeline {
    agent any
    environment {
        VENV_PATH = 'venv'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Kuraye/PythonPipeline.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Create and activate virtual environment in one shell session
                    sh '''
                        python -m venv ${VENV_PATH}
                        source ${VENV_PATH}/bin/activate
                        pip install --upgrade pip
                    '''
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Activate the environment and install dependencies
                    sh '''
                        source ${VENV_PATH}/bin/activate
                        pip install -r requirements.txt
                    '''
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Activate virtual environment and run tests
                    sh '''
                        source ${VENV_PATH}/bin/activate
                        pytest
                    '''
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
