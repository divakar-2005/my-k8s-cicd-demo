pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "k8s-cicd-demo"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/divakar-2005/my-k8s-cicd-demo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE}:${BUILD_NUMBER} -t ${DOCKER_IMAGE}:latest ."
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh "kubectl apply -f deployment.yaml --insecure-skip-tls-verify"
                sh "kubectl rollout restart deployment/web-demo-deployment --insecure-skip-tls-verify"
            }
        }
    }
}
