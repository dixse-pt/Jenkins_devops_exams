pipeline {
    environment {
        DOCKER_ID = "jlnlndr17" // Remplacez ceci par votre ID Docker
        DOCKER_TAG = "v.${BUILD_ID}.0" // Nous allons taguer nos images avec le numéro de build actuel pour l'incrémenter de 1 à chaque nouvelle build
    }
    agent any // Jenkins pourra sélectionner tous les agents disponibles
    stages {
        stage('Build et Push Movie Service') {
            environment {
                DOCKER_MOVIE_IMAGE = "movie-service"
            }
            steps {
                script {
                    // Build de l'image pour le service Movie
                    sh "docker build -t $DOCKER_ID/$DOCKER_MOVIE_IMAGE:$DOCKER_TAG ./movie-service"
                    // Pousse de l'image vers Docker Hub
                    sh "docker login -u $DOCKER_ID -p $DOCKER_PASS" // Assurez-vous de définir DOCKER_PASS dans les paramètres Jenkins
                    sh "docker push $DOCKER_ID/$DOCKER_MOVIE_IMAGE:$DOCKER_TAG"
                }
            }
        }
        stage('Build et Push Cast Service') {
            environment {
                DOCKER_CAST_IMAGE = "cast-service"
            }
            steps {
                script {
                    // Build de l'image pour le service Cast
                    sh "docker build -t $DOCKER_ID/$DOCKER_CAST_IMAGE:$DOCKER_TAG ./cast-service"
                    // Pousse de l'image vers Docker Hub
                    sh "docker login -u $DOCKER_ID -p $DOCKER_PASS" // Assurez-vous de définir DOCKER_PASS dans les paramètres Jenkins
                    sh "docker push $DOCKER_ID/$DOCKER_CAST_IMAGE:$DOCKER_TAG"
                }
            }
        }
        stage('Test Acceptance') {
            steps {
                script {
                    // Exécutez vos tests d'acceptation ici
                }
            }
        }
    }

    stage('Deploiement en dev') {
        steps {
            script {
                sh '''
                rm -Rf .kube
                mkdir .kube
                cat $KUBECONFIG > .kube/config
                cp movie-service-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install movie-service movie-service-chart --values=values.yml --namespace dev
                cp cast-service-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install cast-service cast-service-chart --values=values.yml --namespace dev
                cp postgres-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install postgres postgres-chart --values=values.yml --namespace dev
                '''
            }
        }
    }

    stage('Deploiement en QA') {
        steps {
            script {
                sh '''
                rm -Rf .kube
                mkdir .kube
                cat $KUBECONFIG > .kube/config
                cp movie-service-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install movie-service movie-service-chart --values=values.yml --namespace qa
                cp cast-service-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install cast-service cast-service-chart --values=values.yml --namespace qa
                cp postgres-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install postgres postgres-chart --values=values.yml --namespace qa
                '''
            }
        }
    }

    stage('Deploiement en staging') {
        steps {
            script {
                sh '''
                rm -Rf .kube
                mkdir .kube
                cat $KUBECONFIG > .kube/config
                cp movie-service-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install movie-service movie-service-chart --values=values.yml --namespace staging
                cp cast-service-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install cast-service cast-service-chart --values=values.yml --namespace staging
                cp postgres-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install postgres postgres-chart --values=values.yml --namespace staging
                '''
            }
        }
    }

    stage('Deploiement en prod') {
        steps {
            script {
                timeout(time: 15, unit: "MINUTES") {
                    input message: 'Voulez-vous déployer en production ?', ok: 'Oui'
                }
                sh '''
                rm -Rf .kube
                mkdir .kube
                cat $KUBECONFIG > .kube/config
                cp movie-service-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install movie-service movie-service-chart --values=values.yml --namespace prod
                cp cast-service-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install cast-service cast-service-chart --values=values.yml --namespace prod
                cp postgres-chart/values.yaml values.yml
                sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                helm upgrade --install postgres postgres-chart --values=values.yml --namespace prod
                '''
            }
        }
    }
}