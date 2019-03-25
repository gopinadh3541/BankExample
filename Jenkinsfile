node{
   stage('Checkout')
    {
        checkout scm
    }
	stage('Clean')
    {
		
		
			bat "mvn -f Pipeline_test/pom.xml clean"
		

    }
	 stage('Unit Test')
    {
		
		bat "mvn -f Pipeline_test/pom.xml test"
		
    }
    
   
   
    stage('Packaging')
    {
       
		bat "mvn -f Pipeline_test/pom.xml install"
		
    }
	
	
  
   
   stage('Deploy?')
    {
       input 'Proceed to Deploy?'
    }
   
   stage('Deploy')
   {
   
    
		//sh "mvn -f Pipeline_test/pom.xml deploy"
		withCredentials([usernamePassword(credentialsId: 'By_Login', passwordVariable: 'password', usernameVariable: 'username')]) {
	bat "mvn -f Pipeline_test/pom.xml package -Ddeploy.to.weblogic -Ddeploy.for.weblogic"
	}

}
  
	
	stage('Selenium')
	{
		bat "mvn -f SeleniumTest/pom.xml clean test"
	}
 
	
   
}

    
 
