pipeline {
    agent any

    stages {
        stage('Cloning the code') {
            steps {
                git branch: 'main', url: 'https://github.com/chandu1861/practice.git'
            }
        }
        
        stage('Build the Docker image') {
            steps {
                sh 'docker build -t chandana1213/image:latest .'
            }
        }

        stage('Creating Docker container') {
            steps {
                sh 'docker run -d --name c1 -p 9000:80 chandana1213/image:latest'
            }
        }

        stage('Login and Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push chandana1213/image:latest
                    '''
                }
            }
        }
    }
}
