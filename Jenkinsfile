pipeline{
    agent any;
    stages{
        stage("code"){
            steps {
                git url: "https://github.com/rehanshaikh1207/two-tier-flask-app.git", branch: "master"
            }
        }
        stage("build"){
            steps{
            sh "docker build -t two-tier-application ."
            }
        }    
        stage("test"){
            steps{
                echo"testing developers kar denge"
            }
        }
            stage("docker hub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "dockerhub",
                    passwordVariable: "dockerpass",
                    usernameVariable: "dockeruser"
                )]) {
                    sh "docker login -u ${dockeruser} -p ${dockerpass}"
                    sh "docker image tag two-tier-application ${dockeruser}/two-tier-application"
                    sh "docker push ${dockeruser}/two-tier-application"
                }
            }
        }
        stage("deploy"){
            steps{
               sh "docker compose up -d"
            }
        }
    }
    
}
