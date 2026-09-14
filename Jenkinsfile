pipeline{
    agent any
    stages{
        stage("pull code from github"){
            steps{
                git branch:'main',url:'https://github.com/SahilDhiman8072/html_nginx_project_with_jenkins.git'
            }
        }
        stage("build image"){
            steps{
                sh 'docker build -t nginx_static_pro .'
            }
        }
        stage("tag image"){
            steps{
                sh 'docker tag nginx_static_pro:latest sahild42770/nginx_html_jenkins:latest'
            }
        }
    }
}