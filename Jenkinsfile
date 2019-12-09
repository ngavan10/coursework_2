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
				dockerImage = docker.build("ngavan10/coursework_2")
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
		stage ('Deploy Container')
		{
			agent any
			steps{
				sshagent(['ansible-node']) 
				{
					
					script{
						sh "ssh azureuser@13.92.240.73 kubectl delete deploy/coursework_2"
						sh "ssh azureuser@13.92.240.73 kubectl create deployment coursework_2 --image-ngavan10/coursework_2"
						sh "ssh azureuser@13.92.240.73 kubectl get deployments"
						sh "ssh azureuser@13.92.240.73 kubectl get pods"
						
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
