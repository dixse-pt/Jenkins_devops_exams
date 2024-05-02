pipeline {
    agent any

    environment {
        DOCKER_ID = "jlnlndr17"
        DOCKER_TAG = "v.${BUILD_ID}.0"
        DEV_NAMESPACE = "dev"
        QA_NAMESPACE = "qa"
        STAGING_NAMESPACE = "staging"
        PROD_NAMESPACE = "prod"
    }

    stages {
        stage('Deploy to Dev') {
            steps {
                echo 'Deploying to Dev environment'
                script {
                    // Remplacer les variables dans les fichiers de déploiement Helm Chart
                    sh "sed -i 's/{{DOCKER_ID}}/${DOCKER_ID}/g' fastapi/charts/movie-service/templates/deployment.yaml"
                    sh "sed -i 's/{{DOCKER_TAG}}/${DOCKER_TAG}/g' fastapi/charts/movie-service/templates/deployment.yaml"
                    // Appliquer les déploiements Kubernetes
                    deployToKubernetes(
                        kubeconfigId: 'config',
                        configs: 'fastapi/charts/movie-service/templates/deployment.yaml',
                        kubeNamespace: DEV_NAMESPACE,
                        enableConfigSubstitution: true
                    )
                }
            }
        }

        stage('Deploy to QA') {
            steps {
                echo 'Deploying to QA environment'
                script {
                    // Remplacer les variables dans les fichiers de déploiement Helm Chart pour QA si nécessaire
                    sh "sed -i 's/{{DOCKER_ID}}/${DOCKER_ID}/g' fastapi/charts/movie-service-qa/templates/deployment.yaml"
                    sh "sed -i 's/{{DOCKER_TAG}}/${DOCKER_TAG}/g' fastapi/charts/movie-service-qa/templates/deployment.yaml"
                    // Appliquer les déploiements Kubernetes pour QA si nécessaire
                    deployToKubernetes(
                        kubeconfigId: 'config',
                        configs: 'fastapi/charts/movie-service-qa/templates/deployment.yaml',
                        kubeNamespace: QA_NAMESPACE,
                        enableConfigSubstitution: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging environment'
                script {
                    // Remplacer les variables dans les fichiers de déploiement Helm Chart pour Staging si nécessaire
                    sh "sed -i 's/{{DOCKER_ID}}/${DOCKER_ID}/g' fastapi/charts/movie-service-staging/templates/deployment.yaml"
                    sh "sed -i 's/{{DOCKER_TAG}}/${DOCKER_TAG}/g' fastapi/charts/movie-service-staging/templates/deployment.yaml"
                    // Appliquer les déploiements Kubernetes pour Staging si nécessaire
                    deployToKubernetes(
                        kubeconfigId: 'config',
                        configs: 'fastapi/charts/movie-service-staging/templates/deployment.yaml',
                        kubeNamespace: STAGING_NAMESPACE,
                        enableConfigSubstitution: true
                    )
                }
            }
        }

        stage('Deploy to Prod') {
            steps {
                echo 'Deploying to Production environment'
                script {
                    // Remplacer les variables dans les fichiers de déploiement Helm Chart pour Prod si nécessaire
                    sh "sed -i 's/{{DOCKER_ID}}/${DOCKER_ID}/g' fastapi/charts/movie-service-prod/templates/deployment.yaml"
                    sh "sed -i 's/{{DOCKER_TAG}}/${DOCKER_TAG}/g' fastapi/charts/movie-service-prod/templates/deployment.yaml"
                    // Appliquer les déploiements Kubernetes pour Prod si nécessaire
                    deployToKubernetes(
                        kubeconfigId: 'config',
                        configs: 'fastapi/charts/movie-service-prod/templates/deployment.yaml',
                        kubeNamespace: PROD_NAMESPACE,
                        enableConfigSubstitution: true
                    )
                }
            }
        }
    }
}
