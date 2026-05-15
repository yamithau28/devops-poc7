pipeline {
agent any

environment {
IMAGE_NAME = "04052024/poc7-app:latest"
}

stages {

stage('Clone Code') {
steps {
git branch: 'main',
url: 'https://github.com/yamithau28/devops-poc7.git'
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

sh '''
echo $DOCKER_PASS | docker login \
-u $DOCKER_USER --password-stdin
'''
}
}
}

stage('Push Docker Image') {
steps {
sh 'docker push $IMAGE_NAME'
}
}

stage('Deploy Using Ansible') {
steps {
sh '''
/usr/bin/ansible-playbook \
-i /home/ansible/inventory \
/home/ansible/deploy.yml
'''
}
}
}
}
