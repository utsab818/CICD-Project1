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
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198'
                sh 'scp /var/lib/jenkins/workspace/pipeline-demo/* ubuntu@172.31.40.198:/home/ubuntu/'
                }
            }
        }
        stage('Build docker image from docker file in ansible server'){
            steps {
                sshagent(['AAAAA']) {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 cd /home/ubuntu/'
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 sudo docker image build -t $JOB_NAME:v1.$BUILD_ID .'
                }
            }
        }
        stage('Tag docker image'){
            steps {
                sshagent(['AAAAA']) {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 cd /home/ubuntu/'
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 sudo docker image tag $JOB_NAME:v1.$BUILD_ID utsab12312/$JOB_NAME:v1.$BUILD_ID'
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 sudo docker image tag $JOB_NAME:v1.$BUILD_ID utsab12312/$JOB_NAME:latest'
                }
            }
        }
        stage('Push image to dockerhub'){
            steps {
                sshagent(['AAAAA']) {
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 sudo docker login -u utsab12312 -p ${dockerhub}'
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 sudo docker push utsab12312/$JOB_NAME:v1.$BUILD_ID'
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 sudo docker push utsab12312/$JOB_NAME:latest'
                        // remove after pushing to dockerhub
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.198 sudo docker image rm utsab12312/$JOB_NAME:v1.$BUILD_ID utsab12312/$JOB_NAME:latest'
                }     
            }
        }
        }
        stage('Copy files from jenkins to kubernetes server'){
            steps {
                sshagent(['AAAAA']) { 
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.7.34'   
                    sh 'scp /var/lib/jenkins/workspace/pipeline-demo/* ubuntu@172.31.7.34:/home/ubuntu/'   
                }
            }
        }

    }
}
