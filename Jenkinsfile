pipeline {
    environment {
        DOCKER_ID = "fallewi"
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
                deployToKubernetes(namespace: DEV_NAMESPACE, imageName: "fallewi/movie-service", tag: DOCKER_TAG)
                deployToKubernetes(namespace: DEV_NAMESPACE, imageName: "fallewi/cast-service", tag: DOCKER_TAG)
                deployToKubernetes(namespace: DEV_NAMESPACE, imageName: "fallewi/python-microservice-fastapi", tag: DOCKER_TAG)
            }
        }
        stage('Deploy to QA') {
            when {
                branch 'qa'
            }
            steps {
                echo 'Deploying to QA environment'
                deployToKubernetes(namespace: QA_NAMESPACE, imageName: "fallewi/movie-service", tag: DOCKER_TAG)
                deployToKubernetes(namespace: QA_NAMESPACE, imageName: "fallewi/cast-service", tag: DOCKER_TAG)
                deployToKubernetes(namespace: QA_NAMESPACE, imageName: "fallewi/python-microservice-fastapi", tag: DOCKER_TAG)
            }
        }
        stage('Deploy to Staging') {
            when {
                branch 'staging'
            }
            steps {
                echo 'Deploying to Staging environment'
                deployToKubernetes(namespace: STAGING_NAMESPACE, imageName: "fallewi/movie-service", tag: DOCKER_TAG)
                deployToKubernetes(namespace: STAGING_NAMESPACE, imageName: "fallewi/cast-service", tag: DOCKER_TAG)
                deployToKubernetes(namespace: STAGING_NAMESPACE, imageName: "fallewi/python-microservice-fastapi", tag: DOCKER_TAG)
            }
        }
        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to Production environment'
                deployToKubernetes(namespace: PROD_NAMESPACE, imageName: "fallewi/movie-service", tag: DOCKER_TAG)
                deployToKubernetes(namespace: PROD_NAMESPACE, imageName: "fallewi/cast-service", tag: DOCKER_TAG)
                dep
