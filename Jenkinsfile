pipeline {
    // This is a test
     agent any
     stages {
         stage('AWS Credentials') {
             steps{
                 withCredentials([[$class: 'AmazonWebServicesCredentialBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkinsAWS', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                     sh """
                            mkdir -p ~/.aws
                            echo "[default]" >~/.aws/credentials
                            echo "[default]" >~/.boto
                            echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}">>~/.boto
                            echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}">>~/.boto
                            echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}">>~/.aws/credentials
                            echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}">>~/.aws/credentials
                     """
                 }
             }
         }
         stage('Create EC instance') {
             steps{
                 ansiblePlaybook playbook: 'main.yml', inventory: 'inventory'
             }
         }
     }
}
