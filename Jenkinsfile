pipeline {
    agent any

    environment {
    KUBECONFIG = '/var/jenkins_home/.kube/config'
    }

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                sh '''
                whoami
                echo $KUBECONFIG
                kubectl config current-context
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
