pipeline {
    agent { label "dev_user" }
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/saiprasad66/django-notes-app, branch: "main"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t saiprasad23/django_todo_cicd:latest"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/django_todo_cicd:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
