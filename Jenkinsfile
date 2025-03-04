pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "kpkm25/my-flask-app:latest"
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo "Cloning repository..."
                git url: 'https://github.com/KPkm25/Py-JenDock', branch: 'main'
                echo "Repository cloned successfully."
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Starting Docker build..."
                sh "docker build -t ${DOCKER_IMAGE} ."
                echo "Docker image built successfully."
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    echo "Logging into Docker Hub..."
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-creds') {
                        echo "Pushing Docker image..."
                        sh "docker push ${DOCKER_IMAGE}"
                        echo "Docker image pushed successfully."
                    }
                }
            }
        }
    }
}
