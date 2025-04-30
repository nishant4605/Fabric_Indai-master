pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/nishant4605/Fabric_Indai-master'
        BRANCH = 'main'
        DOCKER_HUB_USERNAME = 'nishant12215057'
        DOCKER_HUB_CREDENTIALS_ID = 'dockerhub-creds-id'
        GITHUB_CREDENTIALS_ID = 'github-creds-id'
        COMPOSE_PROJECT_NAME = 'fabric_india_project'
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git branch: "${BRANCH}", credentialsId: "${GITHUB_CREDENTIALS_ID}", url: "${GIT_REPO}"
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    def services = ['backend', 'frontend', 'admin']
                    for (service in services) {
                        def image = "${DOCKER_HUB_USERNAME}/${service}:latest"
                        dir(service) {
                            echo "Building image for ${service}..."
                            sh "docker build -t ${image} ."
                        }
                    }
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: "${DOCKER_HUB_CREDENTIALS_ID}", url: '']) {
                        def services = ['backend', 'frontend', 'admin']
                        for (service in services) {
                            def image = "${DOCKER_HUB_USERNAME}/${service}:latest"
                            echo "Pushing image ${image} to Docker Hub..."
                            sh "docker push ${image}"
                        }
                    }
                }
            }
        }

        stage('Deploy using Docker Compose') {
            steps {
                script {
                    echo 'Preparing .env files if missing...'
                    sh 'cp -n backend/.env.example backend/.env || true'

                    echo 'Shutting down any existing containers...'
                    sh 'docker compose down || true'

                    echo 'Pulling latest images...'
                    sh 'docker compose pull'

                    echo 'Starting containers...'
                    sh 'docker compose up -d'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment completed successfully!'
        }
        failure {
            echo '❌ Build or deployment failed!'
        }
    }
}
