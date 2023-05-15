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
                sshagent(['Ansible_connection']) {
                sh 'ssh -o StrictHostKeyChecking=no ansible@172.31.42.59'
                sh 'scp /var/lib/jenkins/workspace/pipeline-demo/Dockerfile ansible@172.31.42.59:/home/ubuntu/'
            }
            }
        }
        stage('Build docker image from docker file in ansible server'){
            steps {
                sshagent(['Ansible_connection']) {
                sh 'ssh -o StrictHostKeyChecking=no ansible@172.31.42.59 cd /home/ubuntu/'
                sh 'ssh -o StrictHostKeyChecking=no ansible@172.31.42.59 docker image build -t $JOB_NAME:v1.$BUILD_ID .'
            }
            }
        }
    }
}
