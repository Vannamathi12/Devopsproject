pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'coffee-shop'
        DOCKER_TAG = 'latest'
    }

    stages {
        stage('Checkout Code') {
    steps {
        git credentialsId: 'your-credential-id', url: 'https://github.com/Vannamathi12/Devopsproject.git'
    }
}

        }

        stage('Build') {
            steps {
                script {
                    sh './gradlew clean build' // Change to 'mvn clean package' if using Maven
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh './gradlew test' // Change if using a different test framework
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh "docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} your-docker-hub-username/${DOCKER_IMAGE}:${DOCKER_TAG}"
                    sh "docker push your-docker-hub-username/${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh "docker run -d -p 8080:8080 ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for errors.'
        }
    }
}
