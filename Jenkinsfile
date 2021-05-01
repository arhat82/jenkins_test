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
                    sh 'echo "Tu hermana en tanga">/home/ubuntu/hermana.txt'
                }
            }
        }
    }

}