pipeline {
    agent any
    environment {
        imageName = 'jenkins-demo'
        registryCredentialSet = 'dockerhub-lchomatek'
        registryUri = 'http://localhost:5000'
        dockerInstance = ''
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Container image'
                script {
                    dockerInstance = docker.build(imageName)
                }
            }
        }

        stage('Publish') {
            steps {
                echo 'Publishing image'
                script {
                    docker.withRegistry(registryUri) {
                        dockerInstance.push("${env.BUILD_NUMBER}")
                        dockerInstance.push("latest")
                    }
                }
            }
        }
    }
}