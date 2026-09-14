pipeline{
    agent any
    stages{
        stage("pull code from github"){
            steps{
                git branch:'',git url:''
            }
        }
        stage("build image"){
            steps{
                sh 'docker build -t nginx_static .'
            }
        }
        stage("push to docker hub"){
            steps{
                sh 'docker tag nginx_static '
            }
        }
    }
}