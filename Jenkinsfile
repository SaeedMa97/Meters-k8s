pipeline {
    agent any
    
    environment {
        
        GIT_REPO_URL = 'git@github.com:SaeedMa97/Meters-k8s.git'
    }

    stages {
        stage('Checkout') {
            steps {
                
                git url: "${GIT_REPO_URL}"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f meters-br-deployment.yaml'
                    sh 'kubectl apply -f meters-br-service.yaml'
                    sh 'kubectl apply -f mosquitto-deployment.yaml'
                    sh 'kubectl apply -f mosquitto-service.yaml'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    sh 'kubectl get pods'
                    sh 'kubectl get svc'
                }
            }
        }
    }

    post {
        success {
            echo "Deployment was successful!"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}

