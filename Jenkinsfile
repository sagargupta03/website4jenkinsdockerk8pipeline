// Script //
 
node
{
  // agent { label 'staging'}
  // possible options agent any, none , label , my slave name is staging	
  def app
	
        stage('Clone Repository') {

	echo 'Cloning the repository to our workbook....'
        checkout scm
        }

	stage('Build Image') {
	echo 'This builds the actual image....'
	app = docker.build("sagargupta03/website4maythird")
	}

        stage('Test Image') {
        app.inside{
        echo 'Test passed....'
                  }
	}

        stage('Push Image') {
        echo 'Pushing image to Docker Hub....'
	echo 'docker_hub_sglogin is name of Docker credential...'

        docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_sglogin')
	 {
        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
	 }	
	/*echo ${env.BUILD_NUMBER}*/

	}
}
