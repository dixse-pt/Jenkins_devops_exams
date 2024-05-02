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
                    deployToKubernetes(
                        kubeconfigId: 'config', // Identifier of Kubernetes configuration in Jenkins
                        configs: 'kubernetes/dev-configs.yaml', // Path to Kubernetes configuration file
                        kubeNamespace: DEV_NAMESPACE, // Namespace in Kubernetes
                        enableConfigSubstitution: true
                    )
                }
            }
        }
        stage('Deploy to QA') {
            steps {
                echo 'Deploying to QA environment'
                script {
                    deployToKubernetes(
                        kubeconfigId: 'config',
                        configs: 'kubernetes/qa-configs.yaml',
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
                    deployToKubernetes(
                        kubeconfigId: 'config',
                        configs: 'kubernetes/staging-configs.yaml',
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
                    deployToKubernetes(
                        kubeconfigId: 'config',
                        configs: 'kubernetes/prod-configs.yaml',
                        kubeNamespace: PROD_NAMESPACE,
                        enableConfigSubstitution: true
                    )
                }
            }
        }
    }
}
