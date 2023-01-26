pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment {
        registry = "thuyennc/flask"
        registryCredential = 'dockerhub'
    }
    stages {
        stage ('Building image') {
            steps {
                script {
                    def tag = readFile(file: 'version.txt')
                    dockerImage = docker.build registry + ":$tag"
                }
            }
        }
        stage ('Deploy Image') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
