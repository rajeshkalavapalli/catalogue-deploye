pipeline {
    agent {
        node {
            label 'AGENT'
        }
    }

    options {
        timeout(time: 1, unit: 'HOURS') 
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    parameters {
        string(name: 'version', defaultValue: '', description: 'What is the artifact version?')
        string(name: 'environment', defaultValue: 'dev', description: 'What is the environment?')
    }
    
    stages {
        stage ('Print Version') {
            steps {
                sh """
                    echo "Version: ${params.version}"
                    echo "Environment: ${params.environment}"
                """
            }
        }

        stage ('Initialize Terraform') {
            steps {
                sh """
                    cd terraform
                    terraform init --backend-config=${params.environment}/backend.tf -reconfigure
                    
                """
            }
        }

         stage ('plan') {
            steps {
                sh """
                    cd terraform
                    terraform plan -var-file=${params.environment}/${params.environment}.tfvars -var="app_version=${params.version}"
                    
                """
            }
        }

        stage ('apply') {
            steps {
                sh """
                    cd terraform
                    terraform apply -var-file=${params.environment}/${params.environment}.tfvars -var="app_version=${params.version}" -auto-approve
                    
                """
            }
        }
        
    }

    post { 
        always { 
            echo 'I will always execute!'
            deleteDir()
        }
        failure { 
            echo 'I will run when there is a failure!'
        }
        success { 
            echo 'I will run when there is a success!'
        }
    }
}


