pipeline {
    agent any
    environment {
        imageName = 'lchomatek/jenkins-demo'
        registryCredentialSet = 'dockerhub-lchomatek'
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
                    docker.withRegistry('', registryCredentialSet) {
                        dockerInstance.push("${env.BUILD_NUMBER}")
                        dockerInstance.push("latest")
                    }
                }
            }
        }
    }
}