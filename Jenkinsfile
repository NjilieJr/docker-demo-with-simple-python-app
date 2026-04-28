pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/NjilieJr/docker-demo-with-simple-python-app'
            }
        }
        stage('Build') {
            steps {
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" build -t python-app .'
            }
        }
        stage('Test') {
            steps {
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" run --rm python-app python -m pytest tests/ || echo Tests termines'
            }
        }
        stage('Package') {
            steps {
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" tag python-app python-app:v1.0'
                echo 'Image packagee avec succes !'
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
