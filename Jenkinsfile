pipeline {
    agent {
        node {
            label 'AGENT'
        }
    }
    // environment { 
    //     packageVersion = ""
    //     nexusUrl = "172.31.34.109:8081"
    // }

    options {
        timeout(time: 1, unit: 'HOURS') 
        disableConcurrentBuilds()
    }

    parameters {
        string(name: 'version', defaultValue: '', description: 'what is the artifact version ?')
        string(name: 'environment', defaultValue: 'dev', description: 'what is the environment?')

        
    }
    
    stages {
        stage ('print version') {
            steps {
                sh """
                    echo "version: ${params.version}"
                    echo "environment: ${params.environment}"

                """
            }
        }
    }

     stages {
        stage ('init') {
            steps {
                sh """
                    cd terraform 
                    terraform init --backend-config= ${params.version}/backend.tf -reconfigure

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



