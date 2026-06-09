pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                sh '''
                kubectl get nodes
                kubectl create namespace webapps --dry-run=client -o yaml | kubectl apply -f -
                kubectl apply -f deployment-service.yml -n webapps
                '''
            }
        }

        stage('verify Deployment') {
            steps {
                sh '''
                kubectl get pods -n webapps
                kubectl get svc -n webapps
                '''
            }
        }
    }
}
