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
                git branch: "${BRANCH}", credentialsId: "${GITHUB_CREDENTIALS_ID}", url: "${GIT_REPO}"
            }
        }

        stage('Build and Push Images') {
            steps {
                script {
                    def services = ['backend', 'frontend', 'admin']
                    services.each { service ->
                        def imageName = "${DOCKER_HUB_USERNAME}/${service}:latest"
                        dir("${service}") {
                            sh "docker build -t ${imageName} ."
                        }

                        withDockerRegistry([credentialsId: "${DOCKER_HUB_CREDENTIALS_ID}", url: '']) {
                            sh "docker push ${imageName}"
                        }
                    }
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                script {
                    // Optional: Copy env if needed
                    sh 'cp ./backend/.env.example ./backend/.env || true'

                    // Use 'docker compose' instead of deprecated 'docker-compose'
                    sh "docker compose down || true"
                    sh "docker compose pull"
                    sh "docker compose up -d"
                }
            }
        }
    }

    post {
        failure {
            echo 'Build or deployment failed!'
        }
        success {
            echo 'Deployment successful!'
        }
    }
}
