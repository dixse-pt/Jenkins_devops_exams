pipeline {
    agent any
    
    environment {
        KUBECONFIG = credentials("config") // On récupère kubeconfig depuis un fichier secret appelé "config" enregistré dans Jenkins
        DOCKER_TAG = "v1.0.0" // Tag de l'image Docker à utiliser
        DEV_NAMESPACE = "dev"
        QA_NAMESPACE = "qa"
        STAGING_NAMESPACE = "staging"
        PROD_NAMESPACE = "prod"
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build de l'image Docker
                    docker.build("mon_projet:${DOCKER_TAG}")
                }
            }
        }
        
        stage('Deploy to Dev') {
            steps {
                script {
                    // Configuration pour le déploiement en Dev
                    sh '''
                    rm -Rf .kube
                    mkdir .kube
                    cp $KUBECONFIG .kube/config
                    cp fastapi/values.yaml values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                    helm upgrade --install app fastapi --values=values.yml --namespace ${DEV_NAMESPACE}
                    '''
                }
            }
        }
        
        stage('Deploy to QA') {
            steps {
                script {
                    // Configuration pour le déploiement en QA
                    sh '''
                    rm -Rf .kube
                    mkdir .kube
                    cp $KUBECONFIG .kube/config
                    cp fastapi/values.yaml values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                    helm upgrade --install app fastapi --values=values.yml --namespace ${QA_NAMESPACE}
                    '''
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                script {
                    // Configuration pour le déploiement en Staging
                    sh '''
                    rm -Rf .kube
                    mkdir .kube
                    cp $KUBECONFIG .kube/config
                    cp fastapi/values.yaml values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                    helm upgrade --install app fastapi --values=values.yml --namespace ${STAGING_NAMESPACE}
                    '''
                }
            }
        }
        
        stage('Deploy to Prod') {
            steps {
                script {
                    // Configuration pour le déploiement en Prod
                    sh '''
                    rm -Rf .kube
                    mkdir .kube
                    cp $KUBECONFIG .kube/config
                    cp fastapi/values.yaml values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                    helm upgrade --install app fastapi --values=values.yml --namespace ${PROD_NAMESPACE}
                    '''
                }
            }
        }
    }
}
