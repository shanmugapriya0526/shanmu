pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Jeyaganeshdhanasekar/interview-project'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t newimage /var/lib/jenkins/workspace/project'
                sh 'sudo docker tag newimage jeyaganeshd/newimage:latest'
                sh 'sudo docker tag newimage jeyaganeshd/newimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push jeyaganeshd/newimage:latest'
                sh 'sudo docker image push jeyaganeshd/newimage:${BUILD_NUMBER}'

            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/project/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
