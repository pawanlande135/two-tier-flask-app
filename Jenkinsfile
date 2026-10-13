pipeline{
    agent any;
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/pawanlande135/two-tier-flask-app.git", branch: "master"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t flask-app-im ./"

            }
        }
        stage("Test"){
            steps{
                echo "Code has been tested successfully."

            }
        }
		stage("DockerHub Push"){
		    steps{
			withCredentials([usernamePassword(
			credentialsId:"dockerhubcreds",
			passwordVariable: "dockerhubpass"
			usernameVariable:  "dockerhubuser"
			)]){
			sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
			sh "docker image tag flask-app-im ${env.dockerhubuser}/flask-app-im:latest"
			sh "docker push ${env.dockerhubuser}/flask-app-im:latest"
			}
			
			}
		}
        stage("Deploy"){
            steps{
                sh "docker compose up -d "

            }
        }


    }


}
