pipeline {
    agent any

    environment {
        REMOTE_HOST  = '172.31.18.148'
        REMOTE_USER  = 'ec2-user'
    }
    stages {
        stage ('Deploy on DockerHost EC2') {
            steps {
                script {
                    sshagent (credentials: ['172.31.18.148']) {
                        sh """ 
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_HOST}'
                        touch dockerhost_file
                        '
                        """
                    }
                }
            }
        }
    }
}
