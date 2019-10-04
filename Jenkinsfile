node {
   def mvnHome
   stage('code checkout from GIT') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/kurukundaveera/hello-world.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
 
       mvnHome = tool 'mvn'
   }
    
    stage('Testing Sonar') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package sonar:sonar'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
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
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
 
     stage('Deploy to Tomcat') {
      // Run the maven build
    deploy adapters: [tomcat9(credentialsId: '0ec28164-f474-4adc-969f-ac4c5151bdd2', path: '', url: 'http://13.233.50.45:8888/')], contextPath: 'mytomcat', war: '**/*.war'
         } 
}      
