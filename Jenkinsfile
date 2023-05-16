pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                git 'https://github.com/utsab818/CICD-Project1.git'
            }
        }
        stage('Send dockerfile to ansible server'){
            steps {
                sshagent(['AAAAA']) {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.42.59'
                sh 'scp /var/lib/jenkins/workspace/pipeline-demo/Dockerfile ubuntu@172.31.40.198:/home/ubuntu/'
            }
            }
        }
        stage('Build docker image from docker file in ansible server'){
            steps {
                sshagent(['AAAAA']) {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 cd /home/ubuntu/'
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 docker image build -t $JOB_NAME:v1.$BUILD_ID .'
            }
            }
        }
    }
}
