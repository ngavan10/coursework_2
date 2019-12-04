pipeline{
        agent any
        stages {
                stage ('Build') 
		{
                	steps
			{
                        	echo 'Building'
                        }
                }
                stage ('Sonarqube') 
		{
			agent any
			environment 
			{
				scannerHome = tool 'SonarQubeScanner'
			}
                        steps 
			{
                            withSonarQubeEnv('sonarqube')
				{
					sh "${scannerHome}/bin/sonar-scanner"
                        	}
                  
                	}
		}
                stage ('Build Image')
		{
			agent any
			steps 
			{
				def app = docker.build("ngavan10/coursework_2")
			}
		}
		stage ('Push Image')	
		{
			agent any
			steps
			{
				docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials')
			 	{
			   		def app.push("{env.BUILD_NUMBER}")
			   		def app.push("latest")
			 	}
			}
		}
				

         }
}
