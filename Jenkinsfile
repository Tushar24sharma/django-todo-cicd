pipeline {
    agent any
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url: 'https://github.com/Tushar24sharma/django-todo-cicd.git', branch: 'main'


            }
            
        }
        stage("Build"){
            steps {
                echo "Building the Code"
                sh "docker build -t my-notes-app ."
            }
            
        }
        stage("Push to Dockerhub"){
            steps {
                echo "Pushing the images to Dockerhub"
                withCredentials([usernamePassword(credentialsId: "dockerhub",passwordVariable: "dockerHubPass",usernameVariable: "dockerHubUser")]){
                    sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
                    
                }
            }
            
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
