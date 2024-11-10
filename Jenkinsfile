pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
               script {
                    sh 'ssh root@192.168.40.128'
                    sh 'git clone https://github.com/SaeedMa97/Meters-k8s.git'
                }

            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'ssh root@192.168.40.128'
                    sh 'cd Meters-k8s/'
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
                    sh 'ssh root@192.168.40.128'
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

