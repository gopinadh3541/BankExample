node{
   stage('Checkout')
    {
        checkout scm
    }
	stage('Clean')
    {
		
		withMaven(maven: 'ECD Maven 3.3.9 Windows')
		{
			bat "mvn -f Pipeline_test/pom.xml clean"
		}

    }
	 stage('Unit Test')
    {
		withMaven(maven: 'ECD Maven 3.3.9 Windows')
		{
		bat "mvn -f Pipeline_test/pom.xml test"
		}
    }
    
   
   
    stage('Packaging')
    {
        withMaven(maven: 'ECD Maven 3.3.9 Windows')
		{
		bat "mvn -f Pipeline_test/pom.xml install"
		}
    }
	stage('Publish')
	{
	
		withMaven(maven: 'ECD Maven 3.3.9 Windows')
		{
			bat "mvn -f Pipeline_test/pom.xml clean deploy"
		}
		//nexusArtifactUploader artifacts: [[artifactId: 'BankExample', classifier: '', file: './Java-Pipeline-test/Pipeline_test/target/BankExample.war', type: 'war']], credentialsId: '', groupId: 'com.aep.testdemo', nexusUrl: 'abci-prod:8082/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'http://abci-prod:8082/nexus', version: '1.0'
		
	}
	
  
   
   stage('Deploy?')
    {
       input 'Proceed to Deploy?'
    }
   
   stage('Deploy')
   {
   
    withMaven(maven: 'ECD Maven 3.3.9 Windows')
	{
		//sh "mvn -f Pipeline_test/pom.xml deploy"
		withCredentials([usernamePassword(credentialsId: 'Weblogic', passwordVariable: 'wl.password', usernameVariable: 'wl.username')]) {
	bat "mvn -f Pipeline_test/pom.xml package -Ddeploy.to.weblogic -Ddeploy.for.weblogic"
	}

}
   }
 
	
   
}

    
 
