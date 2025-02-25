pipeline {
    agent any  

    environment {
        DOCKER_IMAGE = 'basinenisaikrishna15/jenkins-demo'
        DOCKER_TAG = 'latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/krish-sai15/jenkins-docker-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE:$DOCKER_TAG .'
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'docker-hub-token', variable: 'DOCKER_PASS')]) {  
                        sh 'echo $DOCKER_PASS | docker login -u basinenisaikrishna15 --password-stdin'
                    }
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                script {
                    sh 'docker push $DOCKER_IMAGE:$DOCKER_TAG'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    sh 'docker run -d -p 8080:80 --name myapp $DOCKER_IMAGE:$DOCKER_TAG'
                }
            }
        }
    }
}

