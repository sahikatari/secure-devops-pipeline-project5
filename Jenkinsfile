pipeline {
    agent any

    environment {
        IMAGE = "sahikatari/secure-app"
        TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Cleanup') {
            steps {
                sh 'docker system prune -f || true'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE:$TAG .'
            }
        }

        stage('Scan Image (Trivy)') {
            steps {
                sh '''
                trivy image --exit-code 0 --severity HIGH,CRITICAL $IMAGE:$TAG
                '''
            }
        }

        stage('DockerHub Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $IMAGE:$TAG
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                export KUBECONFIG=/var/lib/jenkins/.kube/config

                kubectl set image deployment/secure-app \
                secure-app=$IMAGE:$TAG

                kubectl rollout status deployment/secure-app
                '''
            }
        }
    }
}
