pipeline{
        agent any
	
        stages {
                stage ('Building Image') 
		{
			steps{
				script{
				docker.build("ngavan10/coursework_2")
				}
			}
		
                        
                }
		stage ('Push Image')
		{
			steps{
				script{
					docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            				push("${env.BUILD_NUMBER}")
            				push("latest")
        			}
				}
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
      
	
				

         }
}
