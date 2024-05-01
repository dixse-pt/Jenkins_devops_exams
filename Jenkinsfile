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
        stage('Build Docker Images') {
            steps {
                script {
                    docker.build("movie-service:$DOCKER_TAG", "./movie-service")
                    docker.build("cast-service:$DOCKER_TAG", "./cast-service")
                    docker.build("nginx:$DOCKER_TAG", "./nginx")
                }
            }
        }
        stage('Push Docker Images') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("movie-service:$DOCKER_TAG").push()
                        docker.image("cast-service:$DOCKER_TAG").push()
                        docker.image("nginx:$DOCKER_TAG").push()
                    }
                }
            }
        }
        stage('Deploy to Dev') {
            when {
                branch 'development'
            }
            steps {
                echo 'Deploying to Dev environment'
                deployToKubernetes(namespace: DEV_NAMESPACE)
            }
        }
        stage('Deploy to QA') {
            when {
                branch 'qa'
            }
            steps {
                echo 'Deploying to QA environment'
                deployToKubernetes(namespace: QA_NAMESPACE)
            }
        }
        stage('Deploy to Staging') {
            when {
                branch 'staging'
            }
            steps {
                echo 'Deploying to Staging environment'
                deployToKubernetes(namespace: STAGING_NAMESPACE)
            }
        }
        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to Production environment'
                deployToKubernetes(namespace: PROD_NAMESPACE)
            }
        }
    }
}

def deployToKubernetes(namespace) {
    // Utiliser kubectl ou Helm pour déployer les ressources dans le namespace spécifié
    // Par exemple :
    sh "kubectl apply -f ./kubernetes/${namespace}"
    // Ou
    // sh "helm upgrade --install myapp ./helm-chart --namespace=${namespace}"
}
