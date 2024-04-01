pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/manojcloud/k8s-project'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t newimage /var/lib/jenkins/workspace/kube'
                sh 'sudo docker tag newimage manoj167/newimage:latest'
                sh 'sudo docker tag newimage manoj167/newimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push manoj167/newimage:latest'
                sh 'sudo docker image push manoj167/newimage:${BUILD_NUMBER}'

            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/kube/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
