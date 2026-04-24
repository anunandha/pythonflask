pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "pythonflask:latest"
    }

    stages {

        stage('git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/anunandha/pythonflask.git'
            }
        }

        stage('build docker image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('run container') {
            steps {
                sh '''
                    docker rm -f flask_app || true
                    docker run -d -p 5000:5000 --name flask_app ${DOCKER_IMAGE}
                '''
            }
        }

    }
}
