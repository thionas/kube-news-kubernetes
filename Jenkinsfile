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
    }  
}
