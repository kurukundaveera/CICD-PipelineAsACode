pipeline {
	    agent any
	    stages {
	        /* "Build" and "Test" stages omitted */
	

	        stage('Build') {
	            steps {
	      git url : 'https://github.com/kurukundaveera/hello-world-war.git'
	            }
	        }
	

	

	        stage('Publish mertics to Sonarqube') {
	            steps {
	                sh "/opt/maven/bin/mvn clean package deploy sonar:sonar"
	            }
	        }
		
		
	        
	        stage('deploy_war_file_to_tomcat_container') {
	            steps {
	                deploy adapters: [tomcat9(credentialsId: '99aa61ea-652a-4b54-b293-e150de4eda21', 
						  path: '', url: 'http://13.233.50.45:8888/')],
				contextPath: null, war: '**/*.war'
	                
	            }
	        }
	    }
	}




