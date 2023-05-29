pipeline {
    environment {
        registry = 'jonlimpw/jenkinsdemoapp'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Build Docker Image') {
            agent any
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        stage('Push Docker Image') {
            agent any
            steps {
                script {
                    withDockerRegistry([ credentialsId: "dockerhubaccount", url: "" ]) {
        dockerImage.push()
            }            
        }

    }
}
