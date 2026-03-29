pipeline {
    agent any

    environment {
        IMAGE = "secure-app"
    }

    stages {

        stage('Cleanup') {
            steps {
                sh 'docker system prune -af || true'
                sh 'rm -rf ~/.minikube || true'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Scan Image') {
            steps {
                sh '''
                trivy image --exit-code 1 --severity HIGH,CRITICAL $IMAGE
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f secure-app || true
                docker run -d -p 30007:5000 --name secure-app $IMAGE
                '''
            }
        }
    }
}
