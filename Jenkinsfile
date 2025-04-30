pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/nishant4605/Fabric_Indai-master'
        BRANCH = 'main'
        DOCKER_HUB_USERNAME = 'nishant12215057'
        DOCKER_HUB_CREDENTIALS_ID = 'dockerhub-creds-id'
        GITHUB_CREDENTIALS_ID = 'github-creds-id'
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning GitHub repository...'
                git branch: "${BRANCH}", credentialsId: "${GITHUB_CREDENTIALS_ID}", url: "${GIT_REPO}"
            }
        }

        stage('Build & Push Docker Images') {
            steps {
                script {
                    def services = ['backend', 'frontend', 'admin']
                    withDockerRegistry([credentialsId: "${DOCKER_HUB_CREDENTIALS_ID}", url: '']) {
                        services.each { service ->
                            def image = "${DOCKER_HUB_USERNAME}/${service}:latest"
                            echo "Building image for ${service}..."
                            dir(service) {
                                sh "docker build -t ${image} ."
                            }
                            echo "Pushing image ${image} to Docker Hub..."
                            sh "docker push ${image}"
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Docker images built and pushed successfully!'
        }
        failure {
            echo '❌ Build or push failed!'
        }
    }
}
