pipeline{
    agent { label 'agent1' }
    
    stages{
        
        stage('code clone'){
            steps{
                git url: 'https://github.com/hashir527/node-todo-cicd.git', branch: 'master'
            }
        }
            
        stage('build and test'){
            steps{
                
                sh 'docker build . -t hashirsyed/node-todo-app-cicd:latest'
                echo "code build successfully"
            }
        }
        
           stage('docker login and image push'){
            steps{
                
                withCredentials([usernamePassword(credentialsId:'dockerHub', passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUser')]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                sh "docker push hashirsyed/node-todo-app-cicd:latest"
                echo "docker login and image push successfully"
                }
            }
        }
        
        stage('deploy'){
            steps{
                
                sh 'docker-compose down && docker-compose up -d'
                echo "code deploy successfully"
            }
        }
    }
}
