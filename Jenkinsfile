pipeline{
	environment{
		dockerImage = ''
	}
        agent any
	
        stages {
                stage ('Building Image') 
		{
			steps{
				script{
				dockerImage = docker.build("ngavan10/cw2:1.0")
				}
			}
		
                        
                }
		stage ('Push Image')
		{
			steps{
				script{
					docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            				dockerImage.push("${env.BUILD_NUMBER}")
            				dockerImage.push("latest")
        			}
				}
			}
		}
		stage ('Deploy container')
		{
			steps{
				build "cw2"
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
