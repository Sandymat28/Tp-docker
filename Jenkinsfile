pipeline{
  agent any

  environment{
    DOCKERHUB_CREDENTIALS = credentials('DOCKER_ACCOUNT')
    DOCKER_IMAGE = 'matsandy/mon-site-web:latest'
    DOCKER_TAG = 'latest'
    //SANDY_CREDENTIALS = credentials('remote_credentials')
      
    HOSTNAME_DEPLOY = '192.168.1.124'
    DEPLOY_USER = 'larissa'
  }
  
  stages{
    stage ('Deploy in staging') {
        steps {
                sshagent(credentials: ['remote_credentials']) {
                    script {
                        // Commandes pour déployer l'image Docker sur la machine distante
                        sh """
                        ssh -o StrictHostKeyChecking=no ${DEPLOY_USER}@${HOSTNAME_DEPLOY} << EOF
                          docker compose down || true
                          docker pull ${DOCKERHUB_CREDENTIALS_USR}/${DOCKER_IMAGE}:${DOCKER_TAG}

                          # Redémarrez les conteneurs avec la nouvelle image
                          docker run -p 8080:8008 -d ${DOCKER_IMAGE}
                        EOF
                        """
                    }
                }
            }
    }
  }

  post{
      always{
        sh 'docker logout'
      }
  }
}
      
