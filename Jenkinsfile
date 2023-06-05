pipeline {
    agent {
        label 'dev-agent'
    }
    stages {
        stage('Code'){
            steps{
                git url: 'https://github.com/nirmalpopat/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t  popatnirmal2233/node-todo-app-cicd:latest'
            }
        }
        stage('Login and Push Image'){
            steps{
                
                echo 'Login into docker hub'
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push popatnirmal2233/node-todo-app-cicd:latest"
                }
            }
        }
        stage('Deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}