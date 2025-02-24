pipeline{
    
    agent{ label "test" }
    
    stages{
        stage("clone code"){
            steps{
               git url: "https://github.com/pawanlande135/two-tier-flask-app.git", branch: "test"
            }
        }
        
        stage("Build"){
            steps{
               sh "docker build -t flask-app ./ "
            }
        }
        
        stage("Test"){
            steps{
                echo "Developer test case de denga"
            }
        }
        
        stage("docker push"){
            steps{
                
                    withCredentials([usernamePassword(
                    credentialsId: "dockerhubcred",
                    passwordVariable: "dockerhubpass",
                    usernameVariable: "dockerhubuserid")])
                
            {
                
                sh "docker login -u ${env.dockerhubuserid} -p ${env.dockerhubpass}"
                sh "docker tag flask-app ${env.dockerhubuserid}/two-tier-flask-app:latest"
                sh "docker push ${env.dockerhubuserid}/two-tier-flask-app:latest"
            }    
            
                
            }
        }
        stage("Deploy"){
            steps{
            sh "docker compose up -d --build flask-app"
            }
        }
    }
    
    
    
}
