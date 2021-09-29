pipeline {
   agent any

   stages {
      stage('Build') {
         steps {
            bat 'mvn clean package'
         }
      }
	  stage('Test') {
         steps {
            bat 'mvn test'
         }
      }
	  	  stage('Deploy to Sandbox') {
         steps {
            bat 'mvn clean deploy -DmuleDeploy -Dcloudhub.username=RS-Training -Dcloudhub.password=Training@123 -Danypoint.environment=Sandbox'
         }
      }
   }
}