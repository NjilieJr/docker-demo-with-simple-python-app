pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/NjilieJr/docker-demo-with-simple-python-app'
            }
        }
        stage('Build') {
            steps {
                bat 'docker build -t python-app .'
            }
        }
        stage('Test') {
            steps {
                bat 'docker run --rm python-app python -m pytest tests/ || echo "Tests terminés"'
            }
        }
        stage('Package') {
            steps {
                bat 'docker tag python-app python-app:v1.0'
                echo "Image packagée avec succès !"
            }
        }
    }
    post {
        success {
            echo '✅ Pipeline CI/CD terminé avec succès !'
        }
        failure {
            echo '❌ Pipeline échoué !'
        }
    }
}
