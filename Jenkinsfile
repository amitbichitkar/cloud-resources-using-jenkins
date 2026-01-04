pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = "ap-south-1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning Git Repository"
                git 'https://github.com/amitbichitkar/cloud-resources-using-jenkins.git'
            }
        }

        stage('Terraform Init') {
            steps {
               sh 'terraform init'
            }
        }

        stage('Terraform Format') {
            steps {
                
                    sh 'terraform fmt'
                }
         }
        

        stage('Terraform Validate') {
            steps {
                
                    sh 'terraform validate'
                
            }
        }

        stage('Terraform Plan') {
            steps {
             
                    sh 'terraform plan'
                
            }
        }

        stage('Terraform Apply (Launch EC2)') {
            steps {
                 
                    sh 'terraform apply -auto-approve'
                
            }
        }

    }

    post {
        success {
            echo "✅ EC2 Launch Successful (No Destroy)"
        }
        failure {
            echo "❌ Pipeline Failed – Check Terraform Logs"
        }
        always {
            echo "Pipeline Completed"
        }
    }
}
