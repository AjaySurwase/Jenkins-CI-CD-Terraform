pipeline {
    agent any

    parameters {
        booleanParam(name: 'autoApprove', defaultValue: false, description: 'Apply automatically without prompt?')
    }

    environment {
        AWS_ACCESS_KEY_ID     = credentials('Access-key')
        AWS_SECRET_ACCESS_KEY = credentials('Secret-Access-Key')
        AWS_DEFAULT_REGION    = 'ap-south-1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AjaySurwase/Jenkins-CI-CD-Terraform.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Apply') {
            steps {
                script {
                    if (!params.autoApprove) {
                        input message: "Approve to apply Terraform plan?"
                    }
                    sh 'terraform apply -auto-approve'
                }
            }
        }
    }
}
