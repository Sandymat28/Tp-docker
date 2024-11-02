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

        stage('Update and Upgrade Packages') {
            steps {
                sshagent(credentials: [SSH_CREDENTIALS_ID]) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${USERNAME}@${SERVER_IP} << 'EOF'
                        sudo apt-get update
                        sudo apt-get upgrade -y
                        EOF
                    """
                }
            }
        }

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


// pipeline {
//     agent any

//     environment {
//         SSH_CREDENTIALS_ID = 'remote_credentials'
//         SERVER_IP = '192.168.1.124'
//         USERNAME = 'larissa'
//     }

//     stages {
//         stage('Verify SSH Connection') {
//             steps {
//                 script {
//                     // Tester la connexion SSH
//                     def sshCommand = """
//                        sudo ssh -t -o StrictHostKeyChecking=no ${USERNAME}@${SERVER_IP} 'echo "Connection successful!"'
//                     """
//                     sh sshCommand
//                 }
//             }
//         }

//         stage('Update and Upgrade Packages') {
//             steps {
//                 script {
//                     // Mettre à jour et mettre à niveau les paquets sur la machine distante
//                     def sshCommand = """
//                         sudo ssh -t -o StrictHostKeyChecking=no ${USERNAME}@${SERVER_IP} << 'EOF'
//                         sudo apt-get update
//                         sudo apt-get upgrade -y
//                         EOF
//                     """
//                     sh sshCommand
//                 }
//             }
//         }

//         stage('Execute Docker Command') {
//             steps {
//                 script {
//                     // Exécuter une commande Docker sur la machine distante
//                     def dockerCommand = "sudo ssh -t -o StrictHostKeyChecking=no ${USERNAME}@${SERVER_IP} 'docker run --rm matsandy/mon-site-web:latest'"
//                     sh dockerCommand
//                 }
//             }
//         }
//     }

//     post {
//         always {
//             echo 'Pipeline terminé.'
//         }
//     }
// }
// pipeline {
//     agent any

//     environment {
//         DOCKERHUB_CREDENTIALS = credentials('DOCKER_ACCOUNT')
//         DOCKER_IMAGE = 'matsandy/mon-site-web'
//         DOCKER_TAG = 'latest'
//     }

//     stages {
//         stage('SSH') {
//             steps {
//                 sshagent(['remote_credentials']) {
//                     sh '''
//                       ssh -t -o StrictHostKeyChecking=no larissa@192.168.1.124 << 'EOF'
//                       echo "${DOCKERHUB_CREDENTIALS_PSW}" | docker login -u "${DOCKERHUB_CREDENTIALS_USR}" --password-stdin
//                       docker pull ${DOCKER_IMAGE}:${DOCKER_TAG}
//                       docker run -p 8089:8080 -d ${DOCKER_IMAGE}:${DOCKER_TAG}
//                       EOF
//                     '''
//                 }
//             }
//         }
//     }
// }


// pipeline {
//     agent any

//     environment {
//         DOCKERHUB_CREDENTIALS = credentials('DOCKER_ACCOUNT')
//         DOCKER_IMAGE = 'matsandy/mon-site-web:latest'
//         DOCKER_TAG = 'latest'
//     }

//     stages {
//         stage('SSH') {
//             steps {
//                 //sshagent(['remote_credentials']) {
//                     sh '''
//                       ssh -t -o StrictHostKeyChecking=no greatness@192.168.1.212 << 'EOF'
//                       docker pull ${DOCKERHUB_CREDENTIALS_USR}/${DOCKER_IMAGE}:${DOCKER_TAG}
//                       docker run -p 8089:8080 -d ${DOCKER_IMAGE}
                      
//                     '''
//             }
//         }
//     }
// }


/*pipeline {
    agent any

    environment{
    DOCKERHUB_CREDENTIALS = credentials('DOCKER_ACCOUNT')
    DOCKER_IMAGE = 'matsandy/mon-site-web:latest'
    DOCKER_TAG = 'latest'
    //HOSTNAME_DEPLOY = '192.168.1.124'
    //DEPLOY_USER = 'larissa'
    }*/
  
    // stages {
    //     stage('SSH') {
    //         steps {
    //             script{
    //             // sshagent(['remote_credentials']) {
    //             // sh 'ssh-add ~/.ssh/id_rsa'
    //                 sh '''
    //                     ssh larissa@192.168.1.124 << EOF
    //                     docker pull ${DOCKERHUB_CREDENTIALS_USR}/${DOCKER_IMAGE}:${DOCKER_TAG}
    //                     docker run -p 8080:8008 -d ${DOCKER_IMAGE}
    //                 '''
    //             }
    //         }
    //     }
    // }
// }



/*pipeline{
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
}*/
