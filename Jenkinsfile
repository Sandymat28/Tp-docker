pipeline {
    agent any

    environment {
        SSH_CREDENTIALS_ID = 'remote_credentials' // ID des credentials SSH dans Jenkins
        SERVER_IP = '192.168.1.124'
        USERNAME = 'larissa'
    }

    stages {
        stage('Verify SSH Connection') {
            steps {
                sshagent(credentials: [SSH_CREDENTIALS_ID]) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${USERNAME}@${SERVER_IP} 'echo "Connection successful!"'
                    """
                }
            }
        }

        // stage('Update and Upgrade Packages') {
        //     steps {
        //         sshagent(credentials: [SSH_CREDENTIALS_ID]) {
        //             sh """
        //                 ssh -o StrictHostKeyChecking=no ${USERNAME}@${SERVER_IP} << 'EOF'
        //                 sudo apt-get update
        //                 sudo apt-get upgrade -y
        //                 EOF
        //             """
        //         }
        //     }
        // }

        stage('Execute Docker Command') {
            steps {
                sshagent(credentials: [SSH_CREDENTIALS_ID]) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${USERNAME}@${SERVER_IP} 'docker run --rm matsandy/mon-site-web:latest'
                    """
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminé.'
        }
    }
}


