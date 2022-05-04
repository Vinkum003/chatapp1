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
        stage("Package") {
            steps {
                sh "/usr/local/bin/mvn clean package"
            }
        }
        stage("Dockerize") {
            steps {
                sh "/usr/local/bin/docker build -t chatapp1:v2 ."
            }
        }
        stage("Docker Tag") {
            steps {
                sh "/usr/local/bin/docker tag chatapp1:v2 us-east1-docker.pkg.dev/homedepot-342320/vinkumorg/chatapp1:v2"               
            }
        }
        stage("Docker Push") {
            steps {
                sh "/usr/local/bin/docker push us-east1-docker.pkg.dev/homedepot-342320/vinkumorg/chatapp1:v2"               
            }
        }
        stage("Get cluster credentials") {
             steps {
                sh "/Users/vinod.avinane/Desktop/Study/GCP/google-cloud-sdk/bin/gcloud container clusters get-credentials homedepot-342320-gke --region=us-east1"
            }
        }
        stage("Deploy app to GKE") {
            steps {
                sh "/usr/local/bin/helm install mychart /Users/vinod.avinane/Desktop/Study/Kaizen/chatapp1/helm/chatapphelm/ --values /Users/vinod.avinane/Desktop/Study/Kaizen/chatapp1/helm/chatapphelm/values.yaml"
            }
        }   
    }
}