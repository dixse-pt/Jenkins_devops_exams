pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Deploy to Dev') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to Dev environment'
                // Étapes de déploiement vers Dev
            }
        }
        
        stage('Deploy to QA') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to QA environment'
                // Étapes de déploiement vers QA
            }
        }
        
        stage('Deploy to Staging') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to Staging environment'
                // Étapes de déploiement vers Staging
            }
        }
        
        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                echo 'Proceed with deployment to Production?'
                input message: "Proceed with deployment to Production?", ok: "Deploy to Production"
                echo 'Deploying to Production environment'
                // Étapes de déploiement vers Prod (validation manuelle requise)
            }
        }
    }
}
