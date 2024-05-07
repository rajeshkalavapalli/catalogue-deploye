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
        string(name: 'version', defaultValue: '1.0.0', description: 'what is the artifact verionb?')
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



