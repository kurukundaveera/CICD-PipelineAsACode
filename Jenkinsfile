pipeline {
    agent any
    stages {
        stage('Checkout') {
         	   steps {
               		git url: 'https://github.com/kurukundaveera/hello-world-war.git'
            }
        }
		
		stage('Build') {
         	   steps {
               		sh "/opt/maven/bin/mvn clean deploy sonar:sonar"
            }
		}
		
		stage('Deploy') {
         	   steps {
               		    deploy adapters: [tomcat9(credentialsId: 'cfd4addd-a3fb-415c-bdd4-e72675703d7e', path: '', url: 'http://13.232.234.128:8888/')], contextPath: null, war: '**/*.war'
					}
		}
		
    }
	
}

