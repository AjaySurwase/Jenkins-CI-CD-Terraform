pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('Access-Key')
        AWS_SECRET_ACCESS_KEY = credentials('Secret-Access-Key')
        AWS_DEFAULT_REGION    = 'ap-south-1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AjaySurwase/Jenkins-CI-CD-Terraform.git'
            }
        }

        stage('Terraform Init & Validate') {
            steps {
                sh 'terraform init'
                sh 'terraform validate'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
                sh 'terraform show -no-color tfplan > tfplan.txt'
                archiveArtifacts artifacts: 'tfplan.txt', fingerprint: true
            }
        }
    }

    post {
        always {
            echo "Plan job completed. Plan saved as tfplan.txt"
        }
    }
}
