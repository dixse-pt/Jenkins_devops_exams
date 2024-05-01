pipeline {
    environment {
        DOCKER_ID = "jlnlndr17"
        DOCKER_TAG = "v.${BUILD_ID}.0"
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
                // Deployment to dev environment
            }
        }
        stage('Deploy to QA') {
            when {
                branch 'qa'
            }
            steps {
                // Deployment to QA environment
            }
        }
        stage('Deploy to Staging') {
            when {
                branch 'staging'
            }
            steps {
                // Deployment to staging environment
            }
        }
        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                timeout(time: 15, unit: "MINUTES") {
                    input message: 'Do you want to deploy to production?', ok: 'Yes'
                }
                // Deployment to production environment
            }
        }
    }
}
