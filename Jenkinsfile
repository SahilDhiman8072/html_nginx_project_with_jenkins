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
                sh 'docker compose build'
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
                        passwordVariable:'dockerpass'
                    )
                ]){
                sh 'echo "$dockerpass" | docker login -u "$dockeruser" --password-stdin'
                }
            }
        }
        stage("push to docker hub"){
            steps{
                sh 'docker tag $image_name $image_name:$BUILD_NUMBER'
                sh 'docker push $image_name:$BUILD_NUMBER'
            }
        }
        stage("run container"){
            steps{
                sh 'docker compose down || true'
                sh 'docker compose up -d'
            }
            post{
               success{
                sh 'docker compose ps'
               } 
            }
        }
    }

}
