pipeline {
    agent { label "slave" }
    stages {
        stage("Code") {
            steps {
                git url: 'https://github.com/shreeveer/django-notes-app', branch: 'main'
            }
        }
        stage("Build") {
            steps {
                script {
                    docker.build("shreeveer/notes-app:latest")
                }
            }
        }
        stage("Push to DockerHub") {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repositories/shreeshail007', 'dockerhub-credentials-id') {
                        docker.image("shreeshail007/notes-app:latest").push()
                    }
                }
            }
        }
        stage("Deploy") {
            steps {
                echo "This is deploying the code"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

