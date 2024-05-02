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
        //     }
        // }
        stage('Deploiement en dev') {
            steps {
                script {
                    sh '''
                        echo "test"
                    '''
                    // sh '''
                    // rm -Rf .kube
                    // mkdir .kube

                    // cat "$KUBECONFIG" > .kube/config
                    // echo "Chemin kubeconfig : $KUBECONFIG"

                    // cp kubernetes/helm/movie-service-chart/values.yaml values.yml
                    // sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                    // helm upgrade --install movie-service /home/ubuntu/Jenkins_devops_exams/kubernetes/helm/movie-service-chart --values=/home/ubuntu/Jenkins_devops_exams/kubernetes/helm/movie-service-chart/values.yaml --namespace dev
                    // cp kubernetes/helm/cast-service-chart/values.yaml values.yml
                    // sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                    // helm upgrade --install cast-service /home/ubuntu/Jenkins_devops_exams/kubernetes/helm/cast-service-chart --values=/home/ubuntu/Jenkins_devops_exams/kubernetes/helm/cast-service-chart/values.yaml --namespace dev
                    // cp kubernetes/helm/postgresql-chart/values.yaml values.yml
                    // sed -i "s+tag.*+tag: ${DOCKER_TAG}+g" values.yml
                    // helm upgrade --install postgres /home/ubuntu/Jenkins_devops_exams/kubernetes/helm/postgresql-chart --values=/home/ubuntu/Jenkins_devops_exams/kubernetes/helm/postgresql-chart/values.yaml --namespace dev
                    // '''
                }
            }
        }
    }
}
