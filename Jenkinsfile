pipeline {
    agent any
    
    environment {
        DEV_NAMESPACE = "dev"
        QA_NAMESPACE = "qa"
        STAGING_NAMESPACE = "staging"
        PROD_NAMESPACE = "prod"
    }
    
    stages {
        stage('Write to Dev Namespace') {
            steps {
                script {
                    writeFile file: "${DEV_NAMESPACE}-file.txt", text: "This file is written to the ${DEV_NAMESPACE} namespace."
                    echo "File written to ${DEV_NAMESPACE}-file.txt"
                }
            }
        }
        
        stage('Write to QA Namespace') {
            steps {
                script {
                    writeFile file: "${QA_NAMESPACE}-file.txt", text: "This file is written to the ${QA_NAMESPACE} namespace."
                    echo "File written to ${QA_NAMESPACE}-file.txt"
                }
            }
        }
        
        stage('Write to Staging Namespace') {
            steps {
                script {
                    writeFile file: "${STAGING_NAMESPACE}-file.txt", text: "This file is written to the ${STAGING_NAMESPACE} namespace."
                    echo "File written to ${STAGING_NAMESPACE}-file.txt"
                }
            }
        }
        
        stage('Write to Prod Namespace') {
            steps {
                script {
                    writeFile file: "${PROD_NAMESPACE}-file.txt", text: "This file is written to the ${PROD_NAMESPACE} namespace."
                    echo "File written to ${PROD_NAMESPACE}-file.txt"
                }
            }
        }
    }
}
