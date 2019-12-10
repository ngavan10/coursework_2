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
					echo "Building Image"
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
						echo "Push Image"
        			}
				}
			}
		}
		stage ('Deploy container')
		{
			steps{
				build "Deploy Container"
				echo "Deploy To Kubernetes"
			}
		}
                stage ('Scale Application')
                {
                        steps{
                                build "Scale"
                                echo "Scale Application"
                        }
                }
                stage ('Rolling Updates')
                {
                        steps{
                                build "Rolling updates"
                                echo "Rolling Updates"
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
				echo "Testing code"
                  
                	}
		}
                stage ('Clean Up')
                {
                        steps{
                                build "Clean Up"
                                echo "Clean Up"
                        }
                }
      
	
				

         }
}
