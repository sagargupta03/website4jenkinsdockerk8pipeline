pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                }
        }
        stage('Build Docker Image'){
        //    when {
        //        branch 'master'
        //    }
            steps {
                script {
                    app = docker.build("sagargupta03/websiteapache3")
         //           app.inside {
         //               sh 'echo $(curl localhost:8080)'
         //           }
                }
            }
        }
        stage('Pushing Docker Image'){
        //    when {
        //        branch 'master'
        //    }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_sglogin'){
                      app.push("${env.BUILD_NUMBER}")   //build number not including to remove duplicacy in jenkins server images
                        app.push("latest")
                    }
                }
            }
        }
        
       stage('Deploy to Production'){
        //    when {
        //        branch 'master'
        //    }
            steps {
                script{
                echo 'Planning for production run'
                 milestone(1)
                 sh "echo ${env.prod_ip}"
                 sh "ping -c 2 ${env.prod_ip}"  
               ///logic to pull image from docker
                //logic to login to prod server
                //logic to delete before images if any on production
                //logic to run new image on peod ip set in global properties
                
              //  withCredentials([usernamePassword(passwordVariable : 'DOCKER_PASSWORD' ,usernameVariable : 'DOCKER_USERNAME' ,credentialsId : "dockerhub-id" ,)]) {
             //   withCredentials([usernamePassword(passwordVariable : 'DOCKER_PASSWORD' ,usernameVariable : 'DOCKER_USERNAME' ,credentialsId : "docker_hub_sglogin" ,)]) {
              //  withCredentials([usernamePassword(passwordVariable : 'love8win' ,usernameVariable : 'sagargupta03' ,credentialsId : "docker_hub_sglogin" ,)]) {
             //       sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
           //         script{
           //             sh "docker pull sagargupta03/websiteapache3:${env.BUILD_NUMBER}\""
           //         }
                    //logic to run new image on peod ip set in global properties
               //     }
                
                echo 'Run container on production server prod_ip '
               //  def dockerRun = 'docker run -d -p 8080:8080 --name my-app kammana/my-app:0.0.1'
                 def sshCmd = 'ssh -o StrictHostKeyChecking=no ubuntu@${env.prod_ip}'
                 echo $sshCmd
              def dockerRun =  "docker run --restart always --name my-webiste -p 8080:8080 -d sagargupta03/websiteapache3:${env.BUILD_NUMBER}"
                echo $dockerRun
                }
               }
       }
    }
}    
