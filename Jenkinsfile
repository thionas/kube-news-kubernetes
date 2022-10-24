pipeline {
    agent any

    stages {
        stage ('Build Docker image') {
            steps {
                script {
                    dockerapp = docker.build("thionas/kube-news-kubernetes:${env.BUILD_ID}",'-f ./src/Dockerfile ./src')
                }
            }
        }   

        stage ('Push Docker Image') {
            steps {
                script {
                    docker.whitRegistry('https://registry.hub.docker.com', 'dockerhub')
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                }           
            }    
        }

        stage ('Deploy Kubernetes') {
            steps {
                withKubeconfig ([credentialsId: 'kubeconfig']) {
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }               
            }
        }
    }  
}
