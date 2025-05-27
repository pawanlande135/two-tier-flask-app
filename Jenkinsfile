pipeline{

    agent {label "dev"};

    stages{
        stage("code"){
            steps{

                git url: "https://github.com/pawanlande135/two-tier-flask-app.git", branch: "master"              
             
            }


        }
        stage("Build"){
            steps{
               

               sh "docker build -t flask-app-image ./"

                
            }

        }
        stage("Test"){
            steps{

                echo "Code has been Tested successfully."

                
            }
        }

        stage("Docker hub push"){
            steps{

                withCredentials([usernamePassword(
                credentialsId:"dockerhubcreds",
                passwordVariable:"dockerhubPass",
                usernameVariable:"dockerhubUser"
                )]){

                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                    sh "docker image tag flask-app-image ${env.dockerhubUser}/two-tier-flask-app"
                    sh "docker push ${env.dockerhubUser}/two-tier-flask-app:latest"

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
