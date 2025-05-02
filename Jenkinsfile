pipeline {
    agent any

    stages {
        stage("Clonong the Github") {
            steps {
                script {
                    echo "Cloning from Github"
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-token', url: 'https://github.com/sureshv60/MLOPS2.git']])
                }
            }
        }
    }
}