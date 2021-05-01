CODE_CHANGES = getGitChanges()

pipeline{

    agent any

    environment {
        NEW_VERSION = '1.4.5'
        SERVER_CREDENTIALS = credentials('servidor_nuevo')
    }

    stages{
        stage("build"){
            when {
                expression {
                    BRANCH_NAME == 'master' && CODE_CHANGES == true
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
                    BRANCH_NAME == 'master' || BRANCH_NAME == 'dev'
                }
            }

            steps{
                echo "========testing A========"
            }
        }

        stage("deploy"){
            steps{
                echo "========deploying A========"
                echo "Deploying with ${SERVER_CREDENTIALS}"
                sshagent (credentials('servidor_nuevo'))
            }
        }
    }

    post {
        always {
            //Se ejecuta always despues de que se ejecuto el Jenkinsfile
            echo "Always"
        }
        success {
            //Script on success
            echo "Success"
        }
        failure {
            //En caso de failure
            echo "Failure"
        }
    }
}