pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/amitsinghs98/Capstone-Mega-CD-Pipeline.git'
            }  
        }

        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig(
                    credentialsId: 'k8s-cred',
                    clusterName: 'capstone-cluster',
                    namespace: 'webapps',
                    restrictKubeConfigAccess: false,
                    serverUrl: 'https://D133D06C5103AE18A950F2047A8EB7DE.gr7.us-east-1.eks.amazonaws.com'
                ) {
                    sh 'kubectl apply -f kubernetes/Manifest.yaml -n webapps'
                    sh 'kubectl apply -f kubernetes/HPA.yaml'
                    sleep 30
                    sh 'kubectl get pods -n webapps'
                    sh 'kubectl get svc -n webapps'
                }
            }  
        }
    }
}
