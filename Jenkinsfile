pipeline{
    agent any
    environment{
        IMAGE_NAME= "sahild42770/nginx_html_jenkins"
    }
    stages{
        stage("pull code from github"){
            steps{
                git branch:'main',url:'https://github.com/SahilDhiman8072/html_nginx_project_with_jenkins.git'
            }
        }
        stage("build image"){
            steps{
                sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
            }
            post{
                success{
                    sh 'docker images'
                }
            }
        }
        stage("push to dockerhub"){
            steps{
            withCredentials([
                usernamePassword(
                    credentialsId:'dockerhub-up',
                    usernameVariable: 'dockerusername',
                    passwordVariable: 'dockerpass'
                )
            ])
            sh 'echo "$dockerpass" | docker login -u "$dockerusername" --password-stdin' 
            }
        }
        stage("run container"){
            steps{
                sh """
                docker run -d -p 80:80 --name nginx_cont $IMAGE_NAME:$BUILD_NUMBER
                """
            }
        }
    }
}