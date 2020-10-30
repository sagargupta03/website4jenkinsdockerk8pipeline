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
                                   
                echo 'Run container on production server prod_ip '
                 //  sshagent (credentials: ['prod-server-config-k8']) {
                 //  sh "ssh -o StrictHostKeyChecking=no -l jenkins ${env.prod_ip} sudo docker run --restart always --name my-website-latest -p 8080:8080 -d sagargupta03/websiteapache1"
                 //   }
                     kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'website-simple.yaml',
                    enableConfigSubstitution: true
                )
                    
                    
                }
               }
       }
    }
}    
