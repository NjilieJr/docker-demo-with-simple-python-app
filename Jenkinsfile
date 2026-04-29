pipeline {
    agent any

    environment {
        DOCKER_BUILDKIT = '0'
        DOCKER_HOST = 'tcp://localhost:2375'
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
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" -H tcp://localhost:2375 build -t python-app .'
            }
        }
        stage('Test') {
            steps {
                script {
                    def result = bat(
                        script: '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" -H tcp://localhost:2375 run --rm python-app python -m pytest tests/',
                        returnStatus: true
                    )
                    echo "Tests termines avec code: ${result}"
                }
            }
        }
        stage('Package') {
            steps {
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" -H tcp://localhost:2375 tag python-app python-app:v1.0'
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
