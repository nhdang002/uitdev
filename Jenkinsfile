pipeline {
  agent any
  tools { 
        maven 'maven_3_5_2'  
    }
   stages{
    stage('Run Sonar Analysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=scan-sast -Dsonar.organization=uitdevsast -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=24ca391ee110d6ec5ef0ceaad86c2a87c5f9f78b'
		//sh 'mvn clean compile sonar:sonar -Dsonar.projectKey=franksast -Dsonar.organization=franksast -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=ce3caf6f60b599b72a6ced8a5fc17e060b1d87ee'
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
