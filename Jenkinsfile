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
      
	
				

         }
}
