pipeline {
  agent any
  tools { 
        maven 'maven_3_5_2'  
    }
   stages{
    stage('Run Sonar Analysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=scan-sast -Dsonar.organization=uitdevsast -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=24ca391ee110d6ec5ef0ceaad86c2a87c5f9f78b'
		sh 'mvn clean compile sonar:sonar -Dsonar.projectKey=scan-sast -Dsonar.organization=uitdevsast -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=24ca391ee110d6ec5ef0ceaad86c2a87c5f9f78b'
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
