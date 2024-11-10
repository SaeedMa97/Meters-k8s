pipeline {
    agent any

    environment {
        SSH_USER = 'root'
        SSH_HOST = '192.168.40.128'
        REPO_URL = 'https://github.com/SaeedMa97/Meters-k8s.git'
        K8S_DIR = 'Meters-k8s'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    sh """
                        ssh  ${SSH_USER}@${SSH_HOST} "
                            git clone ${REPO_URL}
                        "
                    """
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh """
                        ssh ${SSH_USER}@${SSH_HOST} "
                            cd ${K8S_DIR} && \
                            kubectl apply -f meters-br-deployment.yaml && \
                            kubectl apply -f mosquitto-deployment.yaml
                        "
                    """
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    // Verify pods and services are running
                    sh """
                        ssh  ${SSH_USER}@${SSH_HOST} "
                            kubectl get pods && \
                            kubectl get svc
                        "
                    """
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

