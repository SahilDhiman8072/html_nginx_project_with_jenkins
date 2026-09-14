pipeline{
    agent any
    stages{
        stage("pull code from github"){
            steps{
                git branch:'main',git url:'https://github.com/SahilDhiman8072/html_nginx_project_with_jenkins.git'
            }
        }
        stage("build image"){
            steps{
                sh 'docker build -t nginx_static_pro .'
            }
        }
    }
}