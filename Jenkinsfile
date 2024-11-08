pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Cleanup') {
            steps {
                script {
                    sh 'docker-compose down'
                    sh 'docker rmi -f docker-project_flask_app || true'
                    sh 'docker rmi -f docker-project_mariadb || true'
                }
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executado com sucesso!'
        }
        failure {
            echo 'Pipeline falhou.'
        }
    }
}
