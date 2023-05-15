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
                sshagent(['ansible_demo']) {
                sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.234.114.61'
                sh 'scp /var/lib/jenkins/workspace/pipeline-demo/* ubuntu@13.234.114.61:/home/ubuntu'
                }   
            }
        }
    }
}
