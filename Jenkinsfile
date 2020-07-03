pipeline {
    environment {
        registryCredential = 'dockerhub'
    }
    agent any
    stages {
        stage('Lint') {
            steps {
                sh 'tidy -q -e frontend/*.html'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("ayushpathak01/project4:latest")
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                sh "kubectl set image deployment/project4 devops=ayushpathak01/project4:latest"
            }
        }
    }
}
