pipeline {
    agent any

    // environment {}
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
