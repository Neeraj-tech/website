pipeline {
    agent any
    environment{
        DOCKERHUB_CREDENTIALS=credentials('03e7b12d-0155-4283-878c-5fdd2a8c9dae')
    }

    stages {
        stage('Hello') {
            agent {
                label 'kub_m'
            }
            steps{
                echo 'Hello World'
            }
        }
        
        stage('git') {
            agent {
                label 'kub_m'
            }
            steps{
                git 'https://github.com/Neeraj-tech/website.git'
            }
        }
        
        stage('docker') {
            agent {
                label 'kub_m'
            }
            steps{
                sh 'sudo docker build /home/ubuntu/jenkins/workspace/pipeline -t harodia/capstone'
                sh 'sudo echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'sudo docker push harodia/capstone'
            }
        }
        
        stage('kubernetes') {
            agent {
                label 'kub_m'
            }
            steps{
                sh 'kubectl create -f deploy.yml'
                sh 'kubectl create -f svc.yml'
            }
        }
    }
}
