pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/sahikatari/secure-devops-pipeline-project5.git'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t secure-app .'
            }
        }
    }
}
