node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/kurukundaveera/insurance_backend.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'MVN_HOME'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
       stage('Deploy to Nexus') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean deploy'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean deploy/)
         }
      }
   }
   stage('Deploy to Tomcat')
   {
    withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
   steps{
   deploy adapters: [tomcat9(credentialsId: '99aa61ea-652a-4b54-b293-e150de4eda21', 
						  path: '', url: 'http://13.233.50.45:8888/')],
				contextPath: null, war: '**/*.war'
   }
   }
   }
   }
   
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }

   stage('Sonar Analysis') {
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" sonar:sonar'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" sonar:sonar/)
         }
      }
   }
}
