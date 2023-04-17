pipeline {
    agent { label 'dev-agent'}

    stages {
        stage('Code') {
            steps {
                git url: 'https://github.com/muskanpareek1999/node_todo_cicd.git', branch: 'main'
            }
        }
        stage('Build & Test') {
            steps {
                sh 'docker build . -t muskanpareek/node-todo-app:latest'
            }
        }
        stage('Login & Push Image to DockerHub') {
            steps {
               echo 'login in to docker hub and pushing image....'
               withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]){
                   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                   sh "docker push muskanpareek/node-todo-app:latest"
               }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose down && docker-compose up -d'   
            }
        }
    }
}    
