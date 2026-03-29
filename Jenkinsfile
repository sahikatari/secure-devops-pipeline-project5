pipeline {
    agent any

    environment {
        IMAGE = "sahikatari/secure-app:latest"
        DEPLOYMENT = "secure-app"
        CONTAINER = "secure-app"
    }

    stages {

        stage('Cleanup') {
            steps {
                sh 'docker system prune -f || true'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

       stage('Scan Image (Trivy)') {
    steps {
        sh '''
        trivy image --exit-code 0 --severity HIGH,CRITICAL $IMAGE
        '''
    }
}

        stage('DockerHub Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $IMAGE
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl set image deployment/$DEPLOYMENT $CONTAINER=$IMAGE
                kubectl rollout status deployment/$DEPLOYMENT
                '''
            }
        }
    }
}
