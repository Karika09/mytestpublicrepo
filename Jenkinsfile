pipeline {
    agent any

    environment {
        IMAGE_NAME = 'jenkins-demo-app'
        CONTAINER_NAME = 'jenkins-demo-container'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Karika09/mytestpublicrepo.git' // or use local repo
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    // Stop and remove old container if it exists
                    sh "docker rm -f ${CONTAINER_NAME} || true"

                    // Run new container
                    sh """
                        docker run -d --name ${CONTAINER_NAME} -p 3000:3000 ${IMAGE_NAME}
                    """
                }
            }
        }
    }
}
