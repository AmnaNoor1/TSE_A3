pipeline {
    agent any

    stages {
        stage('Build Backend') {
            steps {
                script {
                    docker.build('backend-image', 'backend')
                }
            }
        }
        stage('Build Frontend') {
            steps {
                script {
                    docker.build('frontend-image', 'frontend')
                }
            }
        }
        stage('Run Backend') {
            steps {
                script {
                    docker.image('backend-image').run('-d -p 5555:5555 --name backend-container')
                }
            }
        }
        stage('Run Frontend') {
            steps {
                script {
                    docker.image('frontend-image').run('-d -p 5173:5173 --name frontend-container')
                }
            }
        }
    }

    post {
        always {
            script {
                docker.stop('backend-container')
                docker.rm('backend-container')
                docker.stop('frontend-container')
                docker.rm('frontend-container')
            }
        }
    }
}