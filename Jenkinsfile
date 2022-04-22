pipeline {
    agent any
    environment {
        PROJECT_ID = 'homedepot-342320'
        LOCATION = 'us-east1'
        CREDENTIALS_ID = 'homedepot-342320'
        CLUSTER_NAME = 'homedepot-342320-gke'
    } 
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage("Deploy app to GKE") {
            steps {
                sh "kubectl apply -f k8s-deployment.yaml"
            }
        }
    }   
}
