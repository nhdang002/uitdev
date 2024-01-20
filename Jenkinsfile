pipeline {
  agent any
  tools { 
        maven 'maven_3_5_2'  
    }
   stages{
    stage('Run Sonar Analysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=uitdev -Dsonar.organization=uitdev -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=090f85bb1c1a79a42f175d1196ff32e7baa3b436'
		sh 'mvn clean compile sonar:sonar -Dsonar.projectKey=uidev -Dsonar.organization=uitdev -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=090f85bb1c1a79a42f175d1196ff32e7baa3b436'
			}
        }
    stage('Run SCA Analysis using Snyk') {
            steps {		
			withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
			    sh 'mvn snyk:test -fn'
				}
			}
    }	


  }
}
