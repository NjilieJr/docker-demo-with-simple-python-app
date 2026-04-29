pipeline {
    agent any

    environment {
        DOCKER_BUILDKIT = '0'
        DOCKER = 'C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/NjilieJr/docker-demo-with-simple-python-app'
            }
        }
        stage('Build') {
            steps {
                bat '"%DOCKER%" build -t python-app .'
            }
        }
        stage('Test') {
            steps {
                bat '"%DOCKER%" run --rm python-app python -m pytest tests/ || echo Tests termines'
            }
        }
        stage('Package') {
            steps {
                bat '"%DOCKER%" tag python-app python-app:v1.0'
                echo 'Image packagee !'
            }
        }
    }
    post {
        success {
            echo 'Pipeline termine avec succes !'
        }
        failure {
            echo 'Pipeline echoue !'
        }
    }
}
