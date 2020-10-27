# website
Demo for Jenkins CICD

Jenkins file is using ssh agent and docker push plugins 

1st - Create a docker image for website
2nd - push it to docker hub
3rd - deploy it to prod ip as per configuration in global setting 

now need to try to deploy in the prod_ip which doesn't have ssh connectivity already established

