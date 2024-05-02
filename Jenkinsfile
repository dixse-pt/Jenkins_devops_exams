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
            steps {
                echo 'Deploying to Dev environment'
                script {
                    // Remplacer les variables dans les fichiers de déploiement Helm Chart
                    sh "sed -i 's/{{DOCKER_ID}}/${DOCKER_ID}/g' charts/movie-service/templates/deployment.yaml"
                    sh "sed -i 's/{{DOCKER_TAG}}/${DOCKER_TAG}/g' charts/movie-service/templates/deployment.yaml"
                    // Appliquer les déploiements Kubernetes
                    sh "helm upgrade --install movie-service charts/movie-service -n ${DEV_NAMESPACE} -f values.yaml"
                }
            }
        }
        stage('Deploy to QA') {
            steps {
                echo 'Deploying to QA environment'
                script {
                    // Remplacer les variables dans les fichiers de déploiement Helm Chart
                    sh "sed -i 's/{{DOCKER_ID}}/${DOCKER_ID}/g' charts/movie-service/templates/deployment.yaml"
                    sh "sed -i 's/{{DOCKER_TAG}}/${DOCKER_TAG}/g' charts/movie-service/templates/deployment.yaml"
                    // Appliquer les déploiements Kubernetes
                    sh "helm upgrade --install movie-service charts/movie-service -n ${QA_NAMESPACE} -f values.yaml"
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging environment'
                script {
                    // Remplacer les variables dans les fichiers de déploiement Helm Chart
                    sh "sed -i 's/{{DOCKER_ID}}/${DOCKER_ID}/g' charts/movie-service/templates/deployment.yaml"
                    sh "sed -i 's/{{DOCKER_TAG}}/${DOCKER_TAG}/g' charts/movie-service/templates/deployment.yaml"
                    // Appliquer les déploiements Kubernetes
                    sh "helm upgrade --install movie-service charts/movie-service -n ${STAGING_NAMESPACE} -f values.yaml"
                }
            }
        }
        stage('Deploy to Prod') {
            steps {
                echo 'Deploying to Production environment'
                script {
                    // Remplacer les variables dans les fichiers de déploiement Helm Chart
                    sh "sed -i 's/{{DOCKER_ID}}/${DOCKER_ID}/g' charts/movie-service/templates/deployment.yaml"
                    sh "sed -i 's/{{DOCKER_TAG}}/${DOCKER_TAG}/g' charts/movie-service/templates/deployment.yaml"
                    // Appliquer les déploiements Kubernetes
                    sh "helm upgrade --install movie-service charts/movie-service -n ${PROD_NAMESPACE} -f values.yaml"
                }
            }
        }
    }
}
