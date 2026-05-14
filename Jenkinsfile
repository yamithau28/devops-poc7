pipeline {
agent any

environment {
IMAGE_NAME = "04052024/poc7-app:latest"
}

stages {

stage('Clone Code') {
steps {
git 'https://github.com/yamithau28/devops-poc7'
}
}

stage('Build Docker Image') {
steps {
sh 'docker build -t $IMAGE_NAME .'
}
}

stage('Docker Login') {
steps {
withCredentials([usernamePassword(
credentialsId: 'dockerhub',
usernameVariable: 'DOCKER_USER',
passwordVariable: 'DOCKER_PASS'
)]) {
sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
}
}
}

stage('Push Docker Image') {
steps {
sh 'docker push $IMAGE_NAME'
}
}
}
}
