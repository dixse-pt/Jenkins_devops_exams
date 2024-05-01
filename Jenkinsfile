pipeline {
    environment {
        DOCKER_ID = "jlnlndr17"
        DOCKER_TAG = "v.${BUILD_ID}.0"
        DEV_NAMESPACE = "dev"
        QA_NAMESPACE = "qa"
        STAGING_NAMESPACE = "staging"
        PROD_NAMESPACE = "prod"
    }
    agent any
    stages {
        stage('Deploy to Dev') {
            when {
                branch 'development'
            }
            steps {
                echo 'Deploying to Dev environment'
                // Place your deployment steps here for the development environment
            }
        }
        stage('Deploy to QA') {
            when {
                branch 'qa'
            }
            steps {
                echo 'Deploying to QA environment'
                // Place your deployment steps here for the QA environment
            }
        }
        stage('Deploy to Staging') {
            when {
                branch 'staging'
            }
            steps {
                echo 'Deploying to Staging environment'
                // Place your deployment steps here for the staging environment
            }
        }
        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                script {
                    input message: "Proceed with deployment to Production?", ok: "Deploy to Production"
                    echo 'Deploying to Production environment'
                    // Place your deployment steps here for the production environment
                }
            }
        }
    }
}
