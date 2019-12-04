pipeline{
        agent any
        stages {
                stage ('Build') {
                        steps{
                                echo 'Building'
                        }
                }
                stage ('Sonarqube') {
			environment {
			scannerHome = tool 'SonarQubeScanner'
			}
                        steps {
                            withSonarQubeENV('sonarqube'){
				sh "${scannerHome}/bin/sonar-scanner"
                        }
			timeout(time: 10, unit: 'MINUTES') {
				waitForQualityGate abortPipeline: ture
			}
                  
                }
                
         }
}
