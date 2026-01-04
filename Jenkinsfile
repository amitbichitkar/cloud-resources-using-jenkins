pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = "ap-south-1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning Git Repository"
                git 'https://github.com/USERNAME/cicd-infra-demo.git'
            }
        }

        stage('Terraform Init') {
            steps {
                dir('terraform') {
                    sh 'terraform init'
                }
            }
        }

        stage('Terraform Format') {
            steps {
                dir('terraform') {
                    sh 'terraform fmt'
                }
            }
        }

        stage('Terraform Validate') {
            steps {
                dir('terraform') {
                    sh 'terraform validate'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                dir('terraform') {
                    sh 'terraform plan'
                }
            }
        }

        stage('Terraform Apply (Launch EC2)') {
            steps {
                dir('terraform') {
                    sh 'terraform apply -auto-approve'
                }
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
