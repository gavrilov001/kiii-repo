pipeline {
    agent any
    stages {
        stage('Build image') {
            steps {
                dir("${WORKSPACE}") {
                    sh 'docker build -t vlatko001/kii .'
                }
            }
        }
    }
}
node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("vlatko001/kii")  
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
        }
    }
}
