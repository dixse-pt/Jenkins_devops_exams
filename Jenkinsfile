pipeline {
    agent any
    environment {
        DOCKER_ID = "jlnlndr17"
        DOCKER_TAG = "v.0.${BUILD_ID}"
        DOCKER_PASS = credentials("DOCKER_HUB_PASS")
        KUBECONFIG = credentials("config")
    }
    stages {
        stage('Build et Push Movie Service') {
            steps {
                script {
                    // Build de l'image pour le service Movie
                    sh "docker build -t $DOCKER_ID/movie-service:$DOCKER_TAG ./movie-service"
                    // Pousse de l'image vers Docker Hub
                    sh "docker login -u $DOCKER_ID -p $DOCKER_PASS"
                    sh "docker push $DOCKER_ID/movie-service:$DOCKER_TAG"
                }
            }
        }
        stage('Build et Push Cast Service') {
            steps {
                script {
                    // Build de l'image pour le service Cast
                    sh "docker build -t $DOCKER_ID/cast-service:$DOCKER_TAG ./cast-service"
                    // Pousse de l'image vers Docker Hub
                    sh "docker login -u $DOCKER_ID -p $DOCKER_PASS"
                    sh "docker push $DOCKER_ID/cast-service:$DOCKER_TAG"
                }
            }
        }
        // stage('Test Acceptance') {
        //     steps {
        //         script {
        //             sh '''
        //             curl localhost
        //             '''
        //         }
        //     }ls
        // }

        stage('Deploiement en dev') {
            steps {
                script {
                    sh '''
                    rm -Rf .kube
                    mkdir .kube
                    ls
                    cp cast-service/cast/values.yaml cast_values.yml
                    cp movie-service/movie/values.yaml movie_values.yml
                    cat cast_values.yml
                    cat movie_values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" cast_values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" movie_values.yml
                    helm upgrade --install cast-service ./cast-service/cast --values=cast_values.yml --namespace dev
                    helm upgrade --install movie-service ./movie-service/movie --values=movie_values.yml --namespace dev
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
                    ls
                    cp cast-service/cast/values.yaml cast_values.yml
                    cp movie-service/movie/values.yaml movie_values.yml
                    cat cast_values.yml
                    cat movie_values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" cast_values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" movie_values.yml
                    helm upgrade --install cast-service ./cast-service/cast --values=cast_values.yml --namespace qa
                    helm upgrade --install movie-service ./movie-service/movie --values=movie_values.yml --namespace qa
                    '''
                }
            }
        }

        stage('Deploiement en staging') {
            steps {
                timeout(time: 15, unit: "MINUTES") {
                    input message: 'Do you want to deploy in production ?', ok: 'Yes'
                }
                script {
                    sh '''
                    rm -Rf .kube
                    mkdir .kube
                    ls
                    cp cast-service/cast/values.yaml cast_values.yml
                    cp movie-service/movie/values.yaml movie_values.yml
                    cat cast_values.yml
                    cat movie_values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" cast_values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" movie_values.yml
                    helm upgrade --install cast-service ./cast-service/cast --values=cast_values.yml --namespace staging
                    helm upgrade --install movie-service ./movie-service/movie --values=movie_values.yml --namespace staging
                    '''
                }
            }
        }

        stage('Deploiement en prod') {
            when {
                branch 'master'
            }
            steps {
                script {
                    sh '''
                    rm -Rf .kube
                    mkdir .kube
                    ls
                    cp cast-service/cast/values.yaml cast_values.yml
                    cp movie-service/movie/values.yaml movie_values.yml
                    cat cast_values.yml
                    cat movie_values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" cast_values.yml
                    sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" movie_values.yml
                    helm upgrade --install cast-service ./cast-service/cast --values=cast_values.yml --namespace prod
                    helm upgrade --install movie-service ./movie-service/movie --values=movie_values.yml --namespace prod
                    '''
                }
            }
        }
    }
}
