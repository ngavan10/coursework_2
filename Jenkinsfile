pipeline{
        agent any
        stages {
                stage ('Building Image') 
		{
			agent any
			environment {
    				registry = "ngavan10/coursework_2"
    				registryCredential = ‘dockerhubcredentials’
  			}
		steps{
			script {
          			docker.build registry + ":$BUILD_NUMBER"
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
