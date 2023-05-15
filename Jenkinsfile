pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                git 'https://github.com/utsab818/CICD-Project1.git'
            }
        }
        stage('Send dockerfile to ansible server'){
            sshagent(['ansible']) {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.42.59'
                sh 'scp /var/lib/jenkins/workspace/pipeline-demo/Dockerfile ubuntu@172.31.42.59:/home/ubuntu'
            }
        }
<<<<<<< HEAD
        stage('Build docker image from docker file in ansible server'){
            sshagent(['ansible']) {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.42.59 cd /home/ubuntu/'
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.42.59 docker image build -t $JOB_NAME:v1.$BUILD_ID .'
            }
        }
=======
>>>>>>> 746068591a0a5af63316ad94363a15c0f525af2e
    }
}
