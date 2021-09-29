pipeline {
   agent any
   stages {
      stage('Checkout from GIT') {
         steps {
            git branch: 'main', credentialsId: '8ab70cd8-15e6-4101-92e7-9159c00f4a66', url: 'https://github.com/Inder92/mule-automation-demo.git'
         }
      }
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
	  	  stage('Deploy to DEV') {
         steps {
		 script {
					def userInput
                        try{
						userInput = input(
        id: 'Proceed1', message: 'Approve/Reject' , parameters: [
		[$class:'BooleanParameterDefinition', defaultValue:true, description: '', name: 'Please confirm you agree with this']
		])
    } catch(err){
        def user= err.getCauses()[0].getUser()
		cause err.causes.get(0)
        echo "Aborted by " + cause.getUser().toString()
        userInput = false
        echo 'aborted by [${user}]'
    
    }
                }
            bat 'mvn clean deploy -DmuleDeploy -Dcloudhub.username=RS-Training -Dcloudhub.password=Training@123 -Danypoint.environment=DEV -Dcloudhub.application=dev-mule-automation-demo'
         }
      }
	   stage('Deploy to QA') {
         steps {
            bat 'mvn clean deploy -DmuleDeploy -Dcloudhub.username=RS-Training -Dcloudhub.password=Training@123 -Danypoint.environment=QA -Dcloudhub.application=qa-mule-automation-demo'
         }
      }
}
}