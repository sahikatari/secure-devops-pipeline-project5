pipeline {
agent any

```
environment {
    IMAGE = "secure-app:latest"
}

stages {

    stage('Clone') {
        steps {
            git 'https://github.com/sahikatari/secure-devops-pipeline-project5.git'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t $IMAGE .'
        }
    }

    stage('Trivy Scan (Fail if HIGH/CRITICAL)') {
        steps {
            sh '''
            trivy image --exit-code 1 --severity HIGH,CRITICAL $IMAGE
            '''
        }
    }

    stage('Deploy to Kubernetes') {
        steps {
            sh 'kubectl apply -f deployment.yaml'
            sh 'kubectl apply -f service.yaml'
        }
    }
}
```

}
