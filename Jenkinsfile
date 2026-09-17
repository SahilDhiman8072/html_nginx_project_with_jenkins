pipeline{
    agent any
    environment{
        image_name= "sahild42770/nginx_html_jenkins"
    }
    stages{
        stage("pull code"){
            steps{
            git branch:'main',url:'https://github.com/SahilDhiman8072/html_nginx_project_with_jenkins.git'
        }
        }
        stage("build image"){
            steps{
                sh 'docker build -t $image_name:$BUILD_NUMBER .'
            }
            post{
                success{
                    sh'docker images'
                }
            }
        }
        stage("docker hub login"){
            steps{
                withCredentials([
                    usernamePassword(
                        credentialsId:'dockerhub-up',
                        usernameVariable:'dockeruser',
                        passwordVarible:'dockerpass'
                    )
                ]){
                sh 'echo "$dockerpass" | docker login -u "$dockeruser" --passwd-stdin'
                }
            }
        }
        stage("push to docker hub"){
            steps{
                sh 'docker push $image_name:$BUILD_NUMBER'
            }
        }
        stage("run container"){
            steps{
                sh 'docker rm -f nginx_cont'
                sh 'docker run -d --name nginx_cont -p 80:80 $image_name:$BUILD_NUMBER'
            }
            post{
               success{
                sh 'docker ps'
               } 
            }
        }
    }

}
