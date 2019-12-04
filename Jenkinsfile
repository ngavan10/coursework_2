pipeline{
        agent any
        stages {
                stage ('Build Image') 
		{
		  agent any
		  def app
			steps{
				app = docker.build("ngavan10/coursework_2")	
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
