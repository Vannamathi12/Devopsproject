pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = 'f737ca6a-0539-43c5-a045-a81ca0076902'  // Replace with your Jenkins credentials ID
        GIT_REPO = 'https://github.com/Vannamathi12/Devopsproject.git'
        GIT_BRANCH = 'main'  // Change to 'master' if your repo uses master
        DOCKER_IMAGE = 'vannamathi124/devopsproject'  // Replace with your Docker Hub repo
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    git credentialsId: GIT_CREDENTIALS, url: GIT_REPO, branch: GIT_BRANCH
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package'  // Replace with the correct build command for your project
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'mvn test'  // Replace with the correct test command
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:latest ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'your-dockerhub-credential-id', url: '']) {
                        sh "docker push ${DOCKER_IMAGE}:latest"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'echo Deploying application...'  
                    // Add deployment commands (e.g., Kubernetes, SSH, etc.)
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
