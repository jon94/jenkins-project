pipeline {
    environment {
        registry = 'jonlimpw/jenkinsdemoapp'
        dockerImage = ''
        credentialsId = "dockerhubaccount"
    }
    agent any
    stages {
        stage('Build Docker Image') {
           datadog(tags: ["stage:dockerbuild"]) { 
            steps {
                script {
                    dockerImage = docker.build("$registry:$BUILD_NUMBER")
                }
            }
        }
    }      
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry([credentialsId: credentialsId, url: '']) {
                        dockerImage.push()
                    }
                }
            }
        }
//         stage('Simulate Error') {
//             steps {
//                 script {
//                     error("Error occurred after pushing the Docker image.")
//                 }
//             }
//         }
    }
}
datadog(tags: ["team:backend", "release:canary"])
