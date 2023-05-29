pipeline {
    environment {
        registry = 'jonlimpw/jenkinsdemoapp'
        dockerImage = ''
        credentialsId = "dockerhubaccount"
    }
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    datadog(tags: ["stage;dockerbuild"]) {
                        dockerImage = docker.build("$registry:$BUILD_NUMBER")
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    datadog(tags: ["stage:dockerpush"]) {
                        withDockerRegistry([credentialsId: credentialsId, url: '']) {
                            dockerImage.push()
                        }
                    }
                }
            }
        }
    }
}
