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
                    app = docker.build("sagargupta03/websiteapache1")
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
                   //   app.push("${env.BUILD_NUMBER}")   //build number not including to remove duplicacy in jenkins server images
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
               ///logic to pull image from docker , login to prod server , to run new image on prod ip set in global properties
                    //logic to delete before images if any on production - pending
                        
                echo 'Run container on production server prod_ip '
                  //  sshagent(['prod-server-config']) {  //for jenkins slave
                    //for k8 master ip as prod-ip
                 //   sshagent(['prod-server-config-k8']) {
       //             sshagent (credentials: ['prod-server-config-k8']) {
                   //sh "ssh -o StrictHostKeyChecking=no ubuntu@54.162.75.27 sudo docker run --restart always --name my-webiste -p 80:80 -d sagargupta03/websiteapache4"
                        //dockerproject user created on prod server which is part of docker group
                        //info --sudo usermod -aG docker dockerproject 
                        //info --sudo useradd dockerproject
                        //info --sudo passwd dockerproject
                   // sh "ssh -o StrictHostKeyChecking=no dockerproject@54.152.133.239 sudo docker run --restart always --name my-website-new2 -p 80:80 -d sagargupta03/websiteapache4"
                 //    sh "ssh -o StrictHostKeyChecking=no -l jenkins@${env.prod_ip} sudo -S docker run --restart always --name my-website-latest -p 8080:8080 -d sagargupta03/websiteapache1"
                        //sh "ssh -o StrictHostKeyChecking=no -l jenkins@${env.prod_ip} uname -a"
                      sh "ssh -o StrictHostKeyChecking=no -l jenkins ${env.prod_ip} docker run --restart always --name my-website-latest -p 8080:8080 -d sagargupta03/websiteapache1"
         //           }
                }
               }
       }
    }
}    
