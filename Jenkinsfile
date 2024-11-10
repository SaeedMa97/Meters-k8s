pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
               script {
                    sh 'ssh root@192.168.40.128 && git clone https://github.com/SaeedMa97/Meters-k8s.git'
                }

            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'ssh root@192.168.40.128 && cd Meters-k8s/ && kubectl apply -f meters-br-deployment.yaml && kubectl apply -f mosquitto-deployment.yaml'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    sh 'ssh root@192.168.40.128 && kubectl get pods && kubectl get svc'
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

