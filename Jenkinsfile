def remote = [:]
remote.name = 'test'
remote.host = 'ec2-54-232-62-250.sa-east-1.compute.amazonaws.com'
remote.user = 'ubuntu'
remote.allowAnyHosts = true

pipeline{

    agent any

    environment {
        NEW_VERSION = '1.4.5'
    }

    stages{
        stage("build"){
            when {
                expression {
                    BRANCH_NAME == 'main'
                }
            }

            steps{
                echo "========building A========"
                echo "Building version ${NEW_VERSION}"
            }
        }

        stage("test"){
            when {
                expression {
                    BRANCH_NAME == 'main' || BRANCH_NAME == 'dev'
                }
            }

            steps{
                echo "========testing A========"
            }
        }

        stage("deploy"){
            steps{
                echo "========deploying A========"
                withCredentials([sshUserPrivateKey(credentialsId: 'servidor_nuevo', keyFileVariable: 'SSH_SERVIDOR', passphraseVariable: '', usernameVariable: '')]) {
                    sh "ssh -i ${SSH_SERVIDOR} ubuntu@ec2-54-232-62-250.sa-east-1.compute.amazonaws.com -x 'touch /home/ubuntu/text4.txt'"
                }
            }
        }
    }

}