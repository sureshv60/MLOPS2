pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage("Clonong the Github") {
            steps {
                script {
                    echo "Cloning from Github"
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-token', url: 'https://github.com/sureshv60/MLOPS2.git']])
                }
            }
        }

        stage("Making a virtual environment") {
            steps {
                script {
                    echo "Making a virtual environment"
                    sh '''
                    python -m venv ${VENV_DIR}
                    . ${VENV_DIR}/bin/activate
                    pip install --upgrade pip
                    pip install -e .
                    pip install dvc
                    '''
                    
                }
            }
        }

        stage('DVC pull'){
            steps{
                withCredentials([file(credentialsId: 'gcp-key', variable: 'GOOGLE_APPLICATION_CREDENTIALS')])
                    script {
                        echo "Pulling data from DVC"
                        sh '''
                        . ${VENV_DIR}/bin/activate
                        dvc pull
                        '''
                    }
            }
        }
    }
}