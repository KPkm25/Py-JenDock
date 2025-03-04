pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'kpkm25/my-flask-app:latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url:'https://github.com/KPkm25/Py-JenDock',branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image') {
            steps {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-creds') 
                {                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
    }
}
