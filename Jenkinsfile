pipeline {
    agent any
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/rrajeshkm/project-todo-cicd.git", branch: "main"
                echo 'bhaiyya code clone ho gaya'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t node-app ."
                echo 'code build bhi ho gaya'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning ho gayi'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app-nodejs:latest ${env.dockerHubUser}/node-app-nodejs:latest"
                sh "docker push ${env.dockerHubUser}/node-app-nodejs:latest"
                echo 'image push ho gaya'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose down && docker compose up -d"
                echo 'deployment ho gayi'
            }
        }
    }
}
