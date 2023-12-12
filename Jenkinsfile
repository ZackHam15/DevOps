pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    environment {
        // Define variables here
        dockerImage = 'zahqh/devops:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean install'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build(dockerImage)
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image(dockerImage).push()
                    }
                }
            }
        }
    }
}
