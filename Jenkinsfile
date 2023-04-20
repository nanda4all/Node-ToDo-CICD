pipeline{
    agent {label 'dev-agent'}
    
    stages{
        
        stage('Code'){
         steps{
             git url: 'https://github.com/nanda4all/Node-ToDo-CICD.git', branch: 'main'
         }
        }
        stage('Build and test'){
         steps{
             sh 'docker build . -t premnanda/node-todo-app-cicd:latest'
         }
        }
        stage('Login and push image'){
            steps{
                echo 'Login into dockerhub and pushing image'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push premnanda/node-todo-app-cicd:latest"
                } 
            }
        }
        stage('Deploy'){
         steps{
             sh 'docker-compose down && docker-compose up -d --no-deps --build web'
         }
        }
    }
}
